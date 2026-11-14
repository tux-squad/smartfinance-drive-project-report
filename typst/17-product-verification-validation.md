# Part II: Verification, Validation & Pipeline

# Capítulo VI: Product Verification & Validation

Este capítulo documenta la estrategia de pruebas aplicada al backend de SmartFinance Drive (`smartfinance-drive-platform`), una aplicación Spring Boot 4.1.1 con Java 26 organizada en bounded contexts bajo Domain-Driven Design. Para el hito TB1 se cubren las cuatro secciones de **Testing Suites & Validation**: pruebas unitarias de entidades, pruebas de integración, Behavior-Driven Development y pruebas de sistema.

Los contextos que se consideran *core* son los más críticos para el negocio del marketplace y del simulador financiero:

| Bounded context | Por qué es core |
| --- | --- |
| IAM | Registro, autenticación con JWT y roles; es la puerta de entrada de todo el sistema. |
| Catalog | Gestión de vehículos publicados; el simulador lee de aquí el precio y las características. |
| Financing | Cálculo del cronograma de pagos (método francés), TCEA, TIR, VAN y solicitudes de crédito. |
| Scoring | Evaluación de riesgo crediticio (DTI y nivel de riesgo A/B/C) que ajusta la tasa. |

Además se prueban los *value objects* compartidos (`Money`, `Percent`) porque todos los contextos dependen de ellos para los cálculos monetarios.

**Herramientas de prueba utilizadas**

| Herramienta | Uso |
| --- | --- |
| JUnit Jupiter | Motor de ejecución y aserciones de todas las pruebas. |
| Mockito | Simulación de repositorios, servicios de aplicación y clientes externos. |
| Spring MockMvc (`@WebMvcTest`) | Pruebas de integración de la capa HTTP con Spring Security. |
| Spring Security Test | Simulación de usuarios autenticados y roles (`@WithMockUser`). |
| Cucumber (Gherkin) | Escenarios BDD sobre las reglas de negocio del dominio. |

**Inventario del conjunto de pruebas del repositorio**

El repositorio contiene 90 clases de prueba en `src/test/java` con 405 métodos de prueba (403 anotados con `@Test` y 2 con `@ParameterizedTest`), distribuidos así:

| Bounded context | Clases de prueba | Métodos de prueba |
| --- | ---: | ---: |
| IAM | 24 | 118 |
| Partners | 16 | 96 |
| Analytics | 4 | 32 |
| Billing | 11 | 30 |
| Catalog | 5 | 28 |
| Shared (value objects, seguridad) | 3 | 22 |
| CRM | 4 | 19 |
| Profiles | 6 | 17 |
| Financing | 6 | 16 |
| Scoring | 4 | 12 |
| Projections | 4 | 11 |
| Consultations | 2 | 3 |
| Aplicación (`SmartfinanceDrivePlatformApplicationTests`) | 1 | 1 |

## 6.1. Testing Suites & Validation

### 6.1.1. Core Entities Unit Tests

Las pruebas unitarias de entidades verifican que los agregados, los *value objects* y los servicios de dominio cumplan sus reglas de negocio **en aislamiento**, sin base de datos ni contexto de Spring. Cada prueba construye el objeto directamente y valida el estado resultante o la excepción de dominio (`DomainValidationException`) cuando se viola una invariante.

**Pruebas por contexto**

**IAM**

| Clase probada | Clase de prueba | Pruebas | Comportamientos verificados |
| --- | --- | ---: | --- |
| `User` (aggregate root) | `UserTest` | 4 | Creación con usuario y contraseña válidos y rol `ROLE_USER` por defecto; rechazo de correos inválidos, vacíos o nulos; rechazo de contraseñas vacías o nulas; alta y baja de roles. |
| `UserCommandServiceImpl` | `UserCommandServiceImplTest` | 11 | Asignación de `ROLE_DEALER` y `ROLE_FINANCIAL_INSTITUTION` solo si el RUC está activo, habido y con CIIU correcto; rechazo con CIIU no automotriz o no financiero; verificación corporativa con dominio no autorizado, límite de 5 solicitudes diarias, enfriamiento de 60 segundos y código OTP inválido. |
| `JwtTokenService` | `JwtTokenServiceTest` | 4 | Generación y extracción del usuario desde el JWT; validación de tokens válidos e inválidos; validación por tipo de token (acceso y refresco); rechazo de secretos nulos o menores de 32 caracteres. |

**Catalog**

| Clase probada | Clase de prueba | Pruebas | Comportamientos verificados |
| --- | --- | ---: | --- |
| `Vehicle` (aggregate root) | `VehicleTest` | 7 | Creación válida; rechazo de marca vacía, modelo en blanco, año de fabricación inválido (1899), condición fuera de catálogo y precio nulo; actualización de detalles. |
| `FuzzySearchUtils` | `FuzzySearchUtilsTest` | 4 | Distancia de Levenshtein exacta y con errores tipográficos, similitud por trigramas y coincidencia aproximada para la búsqueda del catálogo. |

**Financing**

| Clase probada | Clase de prueba | Pruebas | Comportamientos verificados |
| --- | --- | ---: | --- |
| `FinancingPlanBuilder` (servicio de dominio) | `FinancingPlanBuilderTest` | 3 | Cronograma francés estándar sin gracia (24 cuotas, monto financiado de 16 000 USD, saldo final cero, TCEA positiva); periodo de gracia total con capitalización de intereses; Compra Inteligente con cuota balón de 9 000 USD al final del plazo. |
| `Simulation` (aggregate root) | `SimulationTest` | 2 | Al crear la simulación se calculan automáticamente el cronograma (24 periodos), el monto financiado, la TCEA, la TIR y el VAN; rechazo de títulos nulos o en blanco. |
| `CreditApplication` (aggregate root) | `CreditApplicationTest` | 5 | Estado inicial `PENDING`; transición `PENDING` → `IN_REVIEW`; imposibilidad de modificar el estado terminal `DISBURSED`, de volver a `PENDING` y de desembolsar sin aprobación previa. |

**Scoring**

| Clase probada | Clase de prueba | Pruebas | Comportamientos verificados |
| --- | --- | ---: | --- |
| `CreditScoringEngine` (servicio de dominio) | `CreditScoringEngineTest` | 4 | Tier A (DTI ≤ 30 %, aprobado, ajuste de tasa de 1.5), Tier B (30 % < DTI ≤ 45 %, aprobado condicionalmente, sin ajuste), Tier C (DTI > 45 %, rechazado, ajuste de 2.5); rechazo de ingreso cero. |
| `CreditScore` (aggregate root) | `CreditScoreTest` | 2 | Evaluación automática del nivel de riesgo y estado al crear el agregado; rechazo de `profileId` nulo o en blanco. |

**Shared (value objects usados por todos los contextos)**

| Clase probada | Clase de prueba | Pruebas | Comportamientos verificados |
| --- | --- | ---: | --- |
| `Money` | `MoneyTest` | 10 | Creación válida y con moneda por defecto; rechazo de importes inválidos; suma y resta; rechazo de operaciones entre monedas distintas; multiplicación por entero y por decimal; comparaciones. |
| `Percent` | `PercentTest` | 6 | Creación válida e inválida, fábricas `of` y `fromDecimal`, conversión a decimal y formato de texto. |

**Ejemplos de pruebas**

**`UserTest` — gestión de roles del agregado `User`**

```java
@DisplayName("User Aggregate Root Unit Tests")
class UserTest {

    @Test
    @DisplayName("Should allow adding and removing roles")
    void shouldAddAndRemoveRoles() {
        User user = new User(new Username("admin@smartfinance.com"), new Password("SecretPassword123!"));

        user.addRole(Roles.ROLE_ADMIN);
        assertEquals(2, user.getRoles().size());
        assertTrue(user.getRoles().contains(Roles.ROLE_ADMIN));

        user.removeRole(Roles.ROLE_ADMIN);
        assertEquals(1, user.getRoles().size());
        assertFalse(user.getRoles().contains(Roles.ROLE_ADMIN));
    }
}
```

**`CreditScoringEngineTest` — clasificación de riesgo por DTI**

```java
@Test
@DisplayName("Should evaluate Tier A (Low Risk) when DTI <= 30%")
void shouldEvaluateTierAWhenDtiIsLow() {
    Money monthlyIncome = Money.of(5000.0, "PEN");
    Money installment = Money.of(1200.0, "PEN"); // DTI = 24%

    CreditScoringEngine.EvaluationResult result = engine.evaluateRisk(monthlyIncome, installment);

    assertEquals(RiskTier.TIER_A, result.riskTier());
    assertEquals(ScoringStatus.APPROVED, result.status());
    assertEquals(new BigDecimal("1.500000"), result.rateAdjustment().value());
    assertTrue(result.dtiRatio().value().compareTo(new BigDecimal("30.0")) <= 0);
}
```

**`FinancingPlanBuilderTest` — cronograma francés sin gracia**

```java
@Test
@DisplayName("Should generate valid French payment schedule for standard credit without grace")
void shouldGenerateStandardPaymentSchedule() {
    // precio 20 000 USD, cuota inicial 20 %, TEA 12 %, 24 meses
    FinancingPlanBuilder.CalculationOutput output = builder.buildPlan(
            vehiclePrice, downPayment, balloon, tea, desgravamen, vehicleInsFee,
            vehicleInsType, loanTermMonths, graceType, graceMonths, initialFees,
            discountRate, startDate
    );

    assertEquals(24, output.periods().size());
    assertEquals(new BigDecimal("16000.00"), output.financedAmount().amount());
    assertEquals(new BigDecimal("4000.00"), output.downPaymentAmount().amount());

    PaymentPeriod lastPeriod = output.periods().get(23);
    assertEquals(new BigDecimal("0.00"), lastPeriod.getFinalBalance().amount());
    assertTrue(output.tcea().value().compareTo(BigDecimal.ZERO) > 0);
}
```

**`CreditApplicationTest` — máquina de estados de la solicitud de crédito**

```java
@Test
@DisplayName("Should throw exception when attempting to change terminal status DISBURSED")
void shouldPreventChangingTerminalDisbursedState() {
    CreditApplication app = createSampleApplication();
    app.updateStatus("PRE_APPROVED", "Pre approved");
    app.updateStatus("DISBURSED", "Disbursed funds");

    assertThrows(DomainValidationException.class, () ->
        app.updateStatus("REJECTED", "Cannot alter terminal state")
    );
}
```

**Ejecución de las pruebas**

Las pruebas se ejecutan con Maven desde la raíz del repositorio `smartfinance-drive-platform` (requiere JDK 26, según `pom.xml`):

```bash
./mvnw test
```

Para ejecutar solo las pruebas unitarias de los contextos core:

```bash
./mvnw test -Dtest="UserTest,UserCommandServiceImplTest,JwtTokenServiceTest,VehicleTest,FuzzySearchUtilsTest,FinancingPlanBuilderTest,SimulationTest,CreditApplicationTest,CreditScoringEngineTest,CreditScoreTest,MoneyTest,PercentTest"
```

| Alcance ejecutado | Pruebas ejecutadas | Exitosas | Fallidas | Omitidas |
| --- | ---: | ---: | ---: | ---: |
| Pruebas unitarias de entidades core (12 clases) | 62 | 62 | 0 | 0 |

**Desglose por bounded context**

| Bounded context | Clases de prueba | Pruebas ejecutadas | Exitosas | Fallidas |
| --- | ---: | ---: | ---: | ---: |
| IAM | 3 | 19 | 19 | 0 |
| Catalog | 2 | 11 | 11 | 0 |
| Financing | 3 | 10 | 10 | 0 |
| Scoring | 2 | 6 | 6 | 0 |
| Shared | 2 | 16 | 16 | 0 |
| **Total** | **12** | **62** | **62** | **0** |

![Figura 6.1](assets/Chapter-6/figura-6-1.png)

### 6.1.2. Core Integration Tests

Las pruebas de integración verifican que los controladores REST interactúen correctamente con la capa de aplicación, con la seguridad de Spring Security y con el manejo de errores, devolviendo los códigos de estado HTTP esperados. Se aplican dos niveles:

1. **Pruebas de controladores con servicios simulados.** Cada controlador se instancia con sus servicios de aplicación simulados con Mockito y se invoca como lo haría Spring MVC. Validan el mapeo recurso ↔ comando/consulta y el código de estado (`201 Created`, `200 OK`, `204 No Content`).
2. **Pruebas de integración de la capa HTTP con `@WebMvcTest` y `MockMvc`.** Levantan el contexto web de Spring con la cadena de seguridad y envían peticiones HTTP reales contra los controladores. Validan autenticación (`401`), autorización por rol y propiedad (`403`), validación de entrada (`400`) y respuestas exitosas (`200`).

**Pruebas de controladores core**

| Controlador | Clase de prueba | Pruebas | Escenarios verificados |
| --- | --- | ---: | --- |
| `AuthenticationController` (IAM) | `AuthenticationControllerTest` | 4 | `201 Created` en registro; `200 OK` con `token` y `refreshToken` en inicio de sesión, renovación de token e inicio de sesión con Google. |
| `VehiclesController` (Catalog) | `VehiclesControllerTest` | 10 | Creación de vehículo; consulta por id, por usuario y propias; subida de imagen (y borrado de la anterior); listado con filtros vacíos; límite de tamaño de página a 50; rechazo de condición de filtro inválida. |
| `SimulationsController` (Financing) | `SimulationsControllerTest` | 3 | `201 Created` al crear la simulación con el cronograma de 24 pagos en la respuesta; `200 OK` al listar; `204 No Content` al eliminar. |
| `CreditApplicationsController` (Financing) | `CreditApplicationsControllerTest` | 1 | Listado de solicitudes de crédito del usuario. |
| `CreditScoresController` (Scoring) | `CreditScoresControllerTest` | 4 | `201 Created` con `riskTier = TIER_A` al evaluar; `200 OK` al listar y al consultar por perfil; `204 No Content` al eliminar. |

**`SimulationsControllerTest` — creación de una simulación (extracto)**

```java
@Test
@DisplayName("Should create simulation and return 201 Created with full payload")
void shouldCreateSimulation() {
    UsernamePasswordAuthenticationToken auth = new UsernamePasswordAuthenticationToken(
            "usr-1", "password", Collections.emptyList()
    );
    auth.setDetails(new SecurityUtils.AuthenticatedUserDetails("usr-1", "usr-1"));
    SecurityContextHolder.getContext().setAuthentication(auth);

    when(simulationCommandService.handle(any(CreateSimulationCommand.class)))
            .thenReturn(Optional.of(sampleSimulation));

    ResponseEntity<SimulationResource> response = simulationsController.createSimulation(resource);

    assertEquals(HttpStatus.CREATED, response.getStatusCode());
    assertEquals("RAV4 BCP 2026", response.getBody().title());
    assertEquals(24, response.getBody().paymentSchedule().size());
}
```

**`CreditScoresControllerTest` — evaluación de riesgo (extracto)**

```java
@Test
@DisplayName("Should evaluate credit score and return 201 Created")
void shouldEvaluateCreditScore() {
    when(creditScoreCommandService.handle(any(EvaluateCreditScoreCommand.class)))
            .thenReturn(Optional.of(sampleScore));

    ResponseEntity<CreditScoreResource> response = creditScoresController.evaluateCreditScore(resource);

    assertEquals(HttpStatus.CREATED, response.getStatusCode());
    assertEquals("prof-100", response.getBody().profileId());
    assertEquals("TIER_A", response.getBody().riskTier());
}
```

**Pruebas de integración HTTP con MockMvc**

| Clase de prueba | Contexto | Pruebas | Escenarios verificados |
| --- | --- | ---: | --- |
| `CorporateVerificationWebMvcSecurityTest` | IAM | 9 | Las consultas y el inicio de verificación corporativa exigen autenticación; con sesión válida responden correctamente; iniciar o confirmar la verificación de otro usuario es `403 Forbidden`, salvo que sea el propio usuario o un administrador. |
| `PhoneVerificationWebMvcTest` | IAM | 4 | Verificación de token de Firebase: éxito, token inválido, token en blanco y servicio no disponible. |
| `FinancialEntitiesWebMvcSecurityTest` | Partners | 6 | `403 Forbidden` al modificar una entidad ajena, al registrar benchmarks de tasas sin ser propietario, al suplantar el `userId` y al subir un logo con rol de usuario; permitido para el rol de institución financiera. |
| `AnalyticsWebMvcSecurityTest` | Analytics | 10 | Un concesionario o un banco solo consulta sus propias métricas (se bloquea el acceso a datos de otro, IDOR); el administrador consulta cualquiera; periodo inválido responde `400 Bad Request`; el panel de administración está vedado a no administradores. |

**`AnalyticsWebMvcSecurityTest` — un concesionario no puede leer las métricas de otro (IDOR)**

```java
@Test
@WithMockUser(username = "dealer-1", roles = "DEALER")
@DisplayName("DEALER attempting IDOR by querying another dealer's ID should be blocked by SpEL with 403 Forbidden")
void dealerCannotQueryOtherDealerMetrics_IdorBlocked() throws Exception {
    when(ownershipChecker.isUserSelfStr(eq("dealer-2"), any())).thenReturn(false);

    mockMvc.perform(get("/api/v1/analytics/dealer").param("dealerUserId", "dealer-2"))
            .andExpect(status().isForbidden());
}
```

**`CorporateVerificationWebMvcSecurityTest` — una consulta sin sesión es rechazada**

```java
@Test
void lookupRequiresAuthentication() throws Exception {
    mockMvc.perform(get("/api/v1/partners/corporate-verification/lookup/20100047218"))
            .andExpect(status().isUnauthorized());
}
```

**Ejecución de las pruebas de integración**

```bash
./mvnw test -Dtest="AuthenticationControllerTest,VehiclesControllerTest,SimulationsControllerTest,CreditApplicationsControllerTest,CreditScoresControllerTest,CorporateVerificationWebMvcSecurityTest,PhoneVerificationWebMvcTest,FinancialEntitiesWebMvcSecurityTest,AnalyticsWebMvcSecurityTest"
```

| Alcance ejecutado | Pruebas ejecutadas | Exitosas | Fallidas | Omitidas |
| --- | ---: | ---: | ---: | ---: |
| Pruebas de integración de controladores (9 clases) | 51 | 51 | 0 | 0 |

**Desglose por bounded context**

| Bounded context | Clases de prueba | Pruebas ejecutadas | Exitosas | Fallidas |
| --- | ---: | ---: | ---: | ---: |
| IAM | 3 | 17 | 17 | 0 |
| Catalog | 1 | 10 | 10 | 0 |
| Financing | 2 | 4 | 4 | 0 |
| Scoring | 1 | 4 | 4 | 0 |
| Partners | 1 | 6 | 6 | 0 |
| Analytics | 1 | 10 | 10 | 0 |
| **Total** | **9** | **51** | **51** | **0** |

![Figura 6.2](assets/Chapter-6/figura-6-2.png)

### 6.1.3. Core Behavior-Driven Development

Con BDD se describe el comportamiento esperado del sistema en lenguaje natural con la sintaxis **Gherkin** (*Given / When / Then*), de modo que el negocio y el equipo técnico compartan la misma especificación. Cada escenario se vincula con código ejecutable mediante *step definitions* en Java, usando **Cucumber** sobre la plataforma JUnit.

Los escenarios se ejecutan contra las reglas de dominio reales (`FinancingPlanBuilder`, `CreditScoringEngine`, `User`, `Vehicle`, `CreditApplication`), por lo que no necesitan base de datos ni servicios externos.

**Configuración**

Dependencias de prueba que se agregan a `pom.xml`:

```xml
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-java</artifactId>
    <version>7.20.1</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-junit-platform-engine</artifactId>
    <version>7.20.1</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.junit.platform</groupId>
    <artifactId>junit-platform-suite</artifactId>
    <scope>test</scope>
</dependency>
```

Estructura de archivos:

```text
src/test
├── java/com/smartfinance/smartfinancedriveplatform/bdd
│   ├── CucumberSuiteTest.java
│   ├── FinancingPlanSteps.java
│   ├── CreditScoringSteps.java
│   ├── UserRegistrationSteps.java
│   ├── VehicleListingSteps.java
│   └── CreditApplicationSteps.java
└── resources/features
    ├── financing-plan.feature
    ├── credit-scoring.feature
    ├── user-registration.feature
    ├── vehicle-listing.feature
    └── credit-application.feature
```

Clase que descubre y ejecuta los archivos `.feature`:

```java
package com.smartfinance.smartfinancedriveplatform.bdd;

import org.junit.platform.suite.api.ConfigurationParameter;
import org.junit.platform.suite.api.IncludeEngines;
import org.junit.platform.suite.api.SelectClasspathResource;
import org.junit.platform.suite.api.Suite;

import static io.cucumber.junit.platform.engine.Constants.GLUE_PROPERTY_NAME;

@Suite
@IncludeEngines("cucumber")
@SelectClasspathResource("features")
@ConfigurationParameter(key = GLUE_PROPERTY_NAME, value = "com.smartfinance.smartfinancedriveplatform.bdd")
class CucumberSuiteTest {
}
```

**Relación entre features y User Stories**

| Feature | Archivo | Escenarios | Bounded context | User Story |
| --- | --- | ---: | --- | --- |
| Registro de usuario | `user-registration.feature` | 3 | IAM | US-05 Registrar cuenta y perfil personal (escenario 2: datos inválidos) |
| Publicación de vehículos en el catálogo | `vehicle-listing.feature` | 4 | Catalog | US-13 Publicar vehículo (escenarios 1 y 2: publicación exitosa y con datos inválidos) |
| Generación del plan de financiamiento | `financing-plan.feature` | 3 | Financing | US-19 Crear simulación de crédito vehicular (cálculo de cuota y cronograma de pagos) |
| Evaluación de riesgo crediticio | `credit-scoring.feature` | 4 | Scoring | US-19 Crear simulación de crédito vehicular (evaluación de ratios y perfil crediticio) |
| Ciclo de vida de la solicitud de crédito | `credit-application.feature` | 5 | Financing | US-22 Evaluar solicitud de crédito |

**Feature 1: Generación del plan de financiamiento**

`src/test/resources/features/financing-plan.feature`

```gherkin
@financing
Feature: Financing plan generation
  As a buyer
  I want a payment schedule calculated from the vehicle price and the credit conditions
  So that I know the installments before applying for a credit

  Scenario: Standard credit without grace period
    Given a vehicle priced at 20000 USD with a 20 percent down payment
    And an annual effective rate of 12 percent over 24 months
    When the financing plan is generated
    Then the financed amount is 16000 USD
    And the schedule has 24 periods
    And the balance after the last period is zero

  Scenario: Credit with a total grace period
    Given a vehicle priced at 15000 USD with a 10 percent down payment
    And an annual effective rate of 14 percent over 12 months
    And a total grace period of 2 months
    When the financing plan is generated
    Then the schedule has 12 periods
    And the first 2 periods capitalize interest without amortizing principal
    And the balance after the last period is zero

  Scenario: Smart Buy credit with a balloon payment
    Given a vehicle priced at 30000 USD with a 20 percent down payment
    And a balloon payment of 30 percent
    And an annual effective rate of 10 percent over 36 months
    When the financing plan is generated
    Then the financed amount is 24000 USD
    And the balloon payment is 9000 USD
    And the schedule has 36 periods
    And the balance after the last period is zero
```

`FinancingPlanSteps.java`

```java
package com.smartfinance.smartfinancedriveplatform.bdd;

import com.smartfinance.smartfinancedriveplatform.financing.domain.model.entities.PaymentPeriod;
import com.smartfinance.smartfinancedriveplatform.financing.domain.model.valueobjects.GracePeriodType;
import com.smartfinance.smartfinancedriveplatform.financing.domain.model.valueobjects.VehicleInsuranceType;
import com.smartfinance.smartfinancedriveplatform.financing.domain.services.FinancingPlanBuilder;
import com.smartfinance.smartfinancedriveplatform.shared.domain.model.valueobjects.Money;
import com.smartfinance.smartfinancedriveplatform.shared.domain.model.valueobjects.Percent;
import io.cucumber.java.en.Given;
import io.cucumber.java.en.Then;
import io.cucumber.java.en.When;

import java.math.BigDecimal;
import java.time.LocalDate;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertTrue;

public class FinancingPlanSteps {

    private Money vehiclePrice;
    private Percent downPayment;
    private Percent balloon = Percent.of(0.0);
    private Percent tea;
    private int termMonths;
    private GracePeriodType graceType = GracePeriodType.NONE;
    private int graceMonths;
    private FinancingPlanBuilder.CalculationOutput output;

    @Given("a vehicle priced at {double} USD with a {double} percent down payment")
    public void aVehiclePricedWithDownPayment(double price, double downPaymentPercent) {
        vehiclePrice = Money.of(price, "USD");
        downPayment = Percent.of(downPaymentPercent);
    }

    @Given("a balloon payment of {double} percent")
    public void aBalloonPayment(double balloonPercent) {
        balloon = Percent.of(balloonPercent);
    }

    @Given("an annual effective rate of {double} percent over {int} months")
    public void anAnnualRateOverMonths(double teaPercent, int months) {
        tea = Percent.of(teaPercent);
        termMonths = months;
    }

    @Given("a total grace period of {int} months")
    public void aTotalGracePeriod(int months) {
        graceType = GracePeriodType.TOTAL;
        graceMonths = months;
    }

    @When("the financing plan is generated")
    public void theFinancingPlanIsGenerated() {
        output = new FinancingPlanBuilder().buildPlan(
                vehiclePrice, downPayment, balloon, tea, Percent.of(0.05),
                Money.of(50.0, "USD"), VehicleInsuranceType.MENSUAL, termMonths,
                graceType, graceMonths, Money.of(100.0, "USD"), Percent.of(10.0),
                LocalDate.of(2026, 1, 1)
        );
    }

    @Then("the financed amount is {double} USD")
    public void theFinancedAmountIs(double expected) {
        assertEquals(0, BigDecimal.valueOf(expected).compareTo(output.financedAmount().amount()));
    }

    @Then("the balloon payment is {double} USD")
    public void theBalloonPaymentIs(double expected) {
        assertEquals(0, BigDecimal.valueOf(expected).compareTo(output.balloonPaymentAmount().amount()));
    }

    @Then("the schedule has {int} periods")
    public void theScheduleHasPeriods(int expected) {
        assertEquals(expected, output.periods().size());
    }

    @Then("the first {int} periods capitalize interest without amortizing principal")
    public void theFirstPeriodsCapitalizeInterest(int count) {
        for (int i = 0; i < count; i++) {
            PaymentPeriod period = output.periods().get(i);
            assertEquals(GracePeriodType.TOTAL, period.getGraceType());
            assertEquals(0, BigDecimal.ZERO.compareTo(period.getPrincipalAmortization().amount()));
            assertTrue(period.getFinalBalance().amount().compareTo(period.getInitialBalance().amount()) > 0);
        }
    }

    @Then("the balance after the last period is zero")
    public void theBalanceAfterTheLastPeriodIsZero() {
        PaymentPeriod last = output.periods().get(output.periods().size() - 1);
        assertEquals(0, BigDecimal.ZERO.compareTo(last.getFinalBalance().amount()));
    }
}
```

**Feature 2: Evaluación de riesgo crediticio**

`src/test/resources/features/credit-scoring.feature`

```gherkin
@scoring
Feature: Credit risk evaluation
  As a financial institution
  I want to classify the customer risk by the debt-to-income ratio
  So that the interest rate is adjusted to the real payment capacity

  Scenario Outline: Risk tier by debt-to-income ratio
    Given a customer with a monthly income of <income> PEN
    And a projected monthly installment of <installment> PEN
    When the credit risk is evaluated
    Then the risk tier is "<tier>"
    And the scoring status is "<status>"

    Examples:
      | income | installment | tier   | status                 |
      | 5000   | 1200        | TIER_A | APPROVED               |
      | 4000   | 1500        | TIER_B | CONDITIONALLY_APPROVED |
      | 3000   | 1800        | TIER_C | REJECTED               |

  Scenario: Customer without income cannot be evaluated
    Given a customer without income
    And a projected monthly installment of 500 PEN
    When the credit risk is evaluated
    Then the evaluation is rejected with a validation error
```

`CreditScoringSteps.java`

```java
package com.smartfinance.smartfinancedriveplatform.bdd;

import com.smartfinance.smartfinancedriveplatform.scoring.domain.services.CreditScoringEngine;
import com.smartfinance.smartfinancedriveplatform.shared.domain.exceptions.DomainValidationException;
import com.smartfinance.smartfinancedriveplatform.shared.domain.model.valueobjects.Money;
import io.cucumber.java.en.Given;
import io.cucumber.java.en.Then;
import io.cucumber.java.en.When;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertInstanceOf;

public class CreditScoringSteps {

    private Money monthlyIncome;
    private Money installment;
    private CreditScoringEngine.EvaluationResult result;
    private Exception failure;

    @Given("a customer with a monthly income of {double} PEN")
    public void aCustomerWithIncome(double income) {
        monthlyIncome = Money.of(income, "PEN");
    }

    @Given("a customer without income")
    public void aCustomerWithoutIncome() {
        monthlyIncome = Money.zero("PEN");
    }

    @Given("a projected monthly installment of {double} PEN")
    public void aProjectedInstallment(double amount) {
        installment = Money.of(amount, "PEN");
    }

    @When("the credit risk is evaluated")
    public void theCreditRiskIsEvaluated() {
        try {
            result = new CreditScoringEngine().evaluateRisk(monthlyIncome, installment);
        } catch (DomainValidationException e) {
            failure = e;
        }
    }

    @Then("the risk tier is {string}")
    public void theRiskTierIs(String tier) {
        assertEquals(tier, result.riskTier().name());
    }

    @Then("the scoring status is {string}")
    public void theScoringStatusIs(String status) {
        assertEquals(status, result.status().name());
    }

    @Then("the evaluation is rejected with a validation error")
    public void theEvaluationIsRejected() {
        assertInstanceOf(DomainValidationException.class, failure);
    }
}
```

**Feature 3: Registro de usuario**

`src/test/resources/features/user-registration.feature`

```gherkin
@iam
Feature: User registration
  As a visitor
  I want to create an account with my email and a password
  So that I can access the platform features

  Scenario: Registration with valid credentials
    Given a registration with email "john.doe@example.com" and password "SecretPassword123!"
    When the user account is created
    Then the account is created with the default user role

  Scenario: Registration with an invalid email
    Given a registration with email "invalid-email-string" and password "SecretPassword123!"
    When the user account is created
    Then the registration is rejected with a validation error

  Scenario: Registration with a blank password
    Given a registration with email "john.doe@example.com" and password ""
    When the user account is created
    Then the registration is rejected with a validation error
```

`UserRegistrationSteps.java`

```java
package com.smartfinance.smartfinancedriveplatform.bdd;

import com.smartfinance.smartfinancedriveplatform.iam.domain.model.aggregates.User;
import com.smartfinance.smartfinancedriveplatform.iam.domain.model.valueobjects.Password;
import com.smartfinance.smartfinancedriveplatform.iam.domain.model.valueobjects.Roles;
import com.smartfinance.smartfinancedriveplatform.iam.domain.model.valueobjects.Username;
import com.smartfinance.smartfinancedriveplatform.shared.domain.exceptions.DomainValidationException;
import io.cucumber.java.en.Given;
import io.cucumber.java.en.Then;
import io.cucumber.java.en.When;

import static org.junit.jupiter.api.Assertions.assertInstanceOf;
import static org.junit.jupiter.api.Assertions.assertNotNull;
import static org.junit.jupiter.api.Assertions.assertTrue;

public class UserRegistrationSteps {

    private String email;
    private String rawPassword;
    private User user;
    private Exception failure;

    @Given("a registration with email {string} and password {string}")
    public void aRegistrationWith(String email, String password) {
        this.email = email;
        this.rawPassword = password;
    }

    @When("the user account is created")
    public void theUserAccountIsCreated() {
        try {
            user = new User(new Username(email), new Password(rawPassword));
        } catch (DomainValidationException e) {
            failure = e;
        }
    }

    @Then("the account is created with the default user role")
    public void theAccountHasTheDefaultRole() {
        assertNotNull(user);
        assertTrue(user.getRoles().contains(Roles.ROLE_USER));
    }

    @Then("the registration is rejected with a validation error")
    public void theRegistrationIsRejected() {
        assertInstanceOf(DomainValidationException.class, failure);
    }
}
```

**Feature 4: Publicación de vehículos en el catálogo**

`src/test/resources/features/vehicle-listing.feature`

```gherkin
@catalog
Feature: Vehicle listing in the catalog
  As a dealership
  I want to publish vehicles with valid data
  So that buyers see reliable brand, model, year and price in the catalog

  Scenario: Publishing a vehicle with valid data
    Given a vehicle with brand "Toyota", model "Corolla", year 2023, condition "NEW" and price 15000 USD
    When the vehicle is published to the catalog
    Then the vehicle is accepted with brand "Toyota" and year 2023

  Scenario Outline: Publishing a vehicle with invalid data
    Given a vehicle with brand "<brand>", model "<model>", year <year>, condition "<condition>" and price 15000 USD
    When the vehicle is published to the catalog
    Then the vehicle is rejected with a validation error

    Examples:
      | brand  | model   | year | condition         |
      |        | Corolla | 2023 | NEW               |
      | Toyota | Corolla | 1899 | NEW               |
      | Toyota | Corolla | 2023 | INVALID_CONDITION |
```

`VehicleListingSteps.java`

```java
package com.smartfinance.smartfinancedriveplatform.bdd;

import com.smartfinance.smartfinancedriveplatform.catalog.domain.model.aggregates.Vehicle;
import com.smartfinance.smartfinancedriveplatform.catalog.domain.model.valueobjects.FinancialEntityId;
import com.smartfinance.smartfinancedriveplatform.catalog.domain.model.valueobjects.UserId;
import com.smartfinance.smartfinancedriveplatform.shared.domain.exceptions.DomainValidationException;
import com.smartfinance.smartfinancedriveplatform.shared.domain.model.valueobjects.Money;
import io.cucumber.java.en.Given;
import io.cucumber.java.en.Then;
import io.cucumber.java.en.When;

import java.util.UUID;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertInstanceOf;
import static org.junit.jupiter.api.Assertions.assertNotNull;

public class VehicleListingSteps {

    private String brand;
    private String model;
    private int year;
    private String condition;
    private Money price;
    private Vehicle vehicle;
    private Exception failure;

    @Given("a vehicle with brand {string}, model {string}, year {int}, condition {string} and price {double} USD")
    public void aVehicleWith(String brand, String model, int year, String condition, double price) {
        this.brand = brand;
        this.model = model;
        this.year = year;
        this.condition = condition;
        this.price = Money.of(price, "USD");
    }

    @When("the vehicle is published to the catalog")
    public void theVehicleIsPublished() {
        try {
            vehicle = new Vehicle(
                    new UserId(UUID.randomUUID()),
                    new FinancialEntityId(UUID.randomUUID()),
                    brand, model, year, condition, price, null
            );
        } catch (DomainValidationException e) {
            failure = e;
        }
    }

    @Then("the vehicle is accepted with brand {string} and year {int}")
    public void theVehicleIsAccepted(String expectedBrand, int expectedYear) {
        assertNotNull(vehicle);
        assertEquals(expectedBrand, vehicle.getBrand());
        assertEquals(expectedYear, vehicle.getManufactureYear());
    }

    @Then("the vehicle is rejected with a validation error")
    public void theVehicleIsRejected() {
        assertInstanceOf(DomainValidationException.class, failure);
    }
}
```

**Feature 5: Ciclo de vida de la solicitud de crédito**

`src/test/resources/features/credit-application.feature`

```gherkin
@financing
Feature: Credit application lifecycle
  As a financial institution
  I want credit applications to follow a controlled status flow
  So that no application is disbursed without being approved

  Scenario: A new application starts as pending
    Given a new credit application
    Then the application status is "PENDING"

  Scenario: An application moves to review
    Given a new credit application
    When the status changes to "IN_REVIEW"
    Then the application status is "IN_REVIEW"

  Scenario: An application in review cannot go back to pending
    Given a new credit application
    And the application was moved to status "IN_REVIEW"
    When the status changes to "PENDING"
    Then the status change is rejected

  Scenario: An application cannot be disbursed without approval
    Given a new credit application
    When the status changes to "DISBURSED"
    Then the status change is rejected

  Scenario: A disbursed application cannot change status
    Given a new credit application
    And the application was moved to status "PRE_APPROVED"
    And the application was moved to status "DISBURSED"
    When the status changes to "REJECTED"
    Then the status change is rejected
```

`CreditApplicationSteps.java`

```java
package com.smartfinance.smartfinancedriveplatform.bdd;

import com.smartfinance.smartfinancedriveplatform.financing.domain.model.aggregates.CreditApplication;
import com.smartfinance.smartfinancedriveplatform.shared.domain.exceptions.DomainValidationException;
import com.smartfinance.smartfinancedriveplatform.shared.domain.model.valueobjects.Money;
import io.cucumber.java.en.Given;
import io.cucumber.java.en.Then;
import io.cucumber.java.en.When;

import java.math.BigDecimal;
import java.util.UUID;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertInstanceOf;

public class CreditApplicationSteps {

    private CreditApplication application;
    private Exception failure;

    @Given("a new credit application")
    public void aNewCreditApplication() {
        application = new CreditApplication(
                "user-123",
                UUID.randomUUID(),
                UUID.randomUUID(),
                UUID.randomUUID(),
                new Money(new BigDecimal("20000.00"), "USD"),
                new Money(new BigDecimal("4000.00"), "USD"),
                36,
                new Money(new BigDecimal("5000.00"), "USD"),
                "EMPLOYED"
        );
    }

    @Given("the application was moved to status {string}")
    public void theApplicationWasMovedTo(String status) {
        application.updateStatus(status, "Scenario setup");
    }

    @When("the status changes to {string}")
    public void theStatusChangesTo(String status) {
        try {
            application.updateStatus(status, "Scenario action");
        } catch (DomainValidationException e) {
            failure = e;
        }
    }

    @Then("the application status is {string}")
    public void theApplicationStatusIs(String status) {
        assertEquals(status, application.getStatus());
    }

    @Then("the status change is rejected")
    public void theStatusChangeIsRejected() {
        assertInstanceOf(DomainValidationException.class, failure);
    }
}
```

**Ejecución de los escenarios BDD**

```bash
./mvnw test -Dtest=CucumberSuiteTest
```

| Alcance ejecutado | Escenarios | Exitosos | Fallidos | Omitidos |
| --- | ---: | ---: | ---: | ---: |
| 5 features (IAM, Catalog, Financing, Scoring) | 19 | 19 | 0 | 0 |

![Figura 6.3](assets/Chapter-6/figura-6-3.png)

### 6.1.4. Core System Tests

Las pruebas de sistema validan la aplicación **completa y en ejecución** (API REST, Spring Security, JWT y base de datos PostgreSQL), recorriendo los flujos de usuario de extremo a extremo a través de la API documentada con OpenAPI/Swagger. A diferencia de las pruebas anteriores, aquí no se simula ningún componente interno.

**Entorno de ejecución**

| Elemento | Valor |
| --- | --- |
| Aplicación | `smartfinance-drive-platform` ejecutándose localmente (`./mvnw spring-boot:run`) |
| Base de datos | PostgreSQL con migraciones Flyway aplicadas al arrancar |
| URL base | `http://localhost:8080` |
| Herramienta cliente | Swagger UI (`/swagger-ui/index.html`) o Postman |
| Autenticación | `Authorization: Bearer <token>` obtenido en `POST /api/v1/auth/sessions` |

**Casos de prueba de sistema**

A continuación se detallan los casos de prueba de sistema diseñados para validar los flujos de extremo a extremo a través de los endpoints de la API RESTful:

- **ST-01 (US-05 — Registro exitoso):**
  - **Petición:** `POST /api/v1/auth/registrations` con correo, contraseña y datos válidos.
  - **Resultado esperado:** `201 Created` con confirmación de cuenta creada.

- **ST-02 (US-05 — Registro con datos inválidos):**
  - **Petición:** `POST /api/v1/auth/registrations` con un correo mal formado.
  - **Resultado esperado:** `400 Bad Request` indicando error de validación.

- **ST-03 (US-07 — Inicio de sesión exitoso):**
  - **Petición:** `POST /api/v1/auth/sessions` con credenciales válidas registradas.
  - **Resultado esperado:** `200 OK` con emisión de `token` y `refreshToken`.

- **ST-04 (US-08 — Cierre de sesión):**
  - **Petición:** `DELETE /api/v1/auth/sessions/current` con `Authorization: Bearer <token>`.
  - **Resultado esperado:** `200 OK` con el mensaje `User signed out successfully`.

- **ST-05 (US-08 — Uso de la sesión anterior tras cerrar sesión):**
  - **Petición:** Intento de consumo de cualquier endpoint protegido reutilizando el token cerrado.
  - **Resultado esperado:** Acceso rechazado con código `401 Unauthorized`.

- **ST-06 (US-10 — Modificar roles como administrador):**
  - **Petición:** `PUT /api/v1/users/{userId}/roles` autenticado con usuario `ROLE_ADMIN`.
  - **Resultado esperado:** `200 OK` con los roles actualizados en el sistema.

- **ST-07 (US-10 — Modificar roles sin ser administrador):**
  - **Petición:** `PUT /api/v1/users/{userId}/roles` autenticado con usuario estándar `ROLE_USER`.
  - **Resultado esperado:** Acceso denegado con código `403 Forbidden`.

- **ST-08 (US-13 — Publicar un vehículo como concesionaria):**
  - **Petición:** `POST /api/v1/vehicles` con usuario `ROLE_DEALER` y datos comerciales válidos.
  - **Resultado esperado:** `201 Created` con el vehículo creado y persistido en inventario.

- **ST-09 (US-13 — Publicar un vehículo con datos inválidos):**
  - **Petición:** `POST /api/v1/vehicles` con año de fabricación inválido (ej. 1899).
  - **Resultado esperado:** `400 Bad Request` impidiendo el registro incorrecto.

- **ST-10 (US-16 — Buscar vehículos con filtros):**
  - **Petición:** `GET /api/v1/vehicles?brand=Toyota&minPrice=10000&maxPrice=30000&condition=NEW`.
  - **Resultado esperado:** `200 OK` con la lista paginada de vehículos que cumplen los filtros.

- **ST-11 (US-18 — Ver el detalle de un vehículo):**
  - **Petición:** `GET /api/v1/vehicles/{vehicleId}` con identificador existente.
  - **Resultado esperado:** `200 OK` con los datos completos de la ficha del vehículo.

- **ST-12 (US-14 — Cambiar el estado de un vehículo ajeno):**
  - **Petición:** `PATCH /api/v1/vehicles/{vehicleId}/status` con una concesionaria no propietaria.
  - **Resultado esperado:** `403 Forbidden` en cumplimiento de la regla `isVehicleOwner`.

- **ST-13 (US-19 — Pre-evaluación de riesgo crediticio):**
  - **Petición:** `POST /api/v1/credit-scores` con ingreso mensual 5 000 PEN y cuota 1 200 PEN.
  - **Resultado esperado:** `201 Created` asignando la categoría `riskTier = TIER_A`.

- **ST-14 (US-19 — Crear una simulación de crédito):**
  - **Petición:** `POST /api/v1/simulations` con precio 25 000 USD, cuota inicial 20 % y plazo de 24 meses.
  - **Resultado esperado:** `201 Created` con cronograma calculado de 24 pagos bajo método francés.

- **ST-15 (US-21 — Eliminar la simulación de otro cliente):**
  - **Petición:** `DELETE /api/v1/simulations/{id}` con un token distinto al del propietario.
  - **Resultado esperado:** `403 Forbidden` en cumplimiento de la regla `isSimulationOwner`.

- **ST-16 (US-22 — Evaluar una solicitud sin ser entidad financiera):**
  - **Petición:** `PATCH /api/v1/credit-applications/{id}/status` con un usuario estándar `ROLE_USER`.
  - **Resultado esperado:** Acceso denegado con código `403 Forbidden`.

- **ST-17 (US-22 — Registrar la evaluación como entidad financiera):**
  - **Petición:** `PATCH /api/v1/credit-applications/{id}/status` con usuario `ROLE_FINANCIAL_INSTITUTION`.
  - **Resultado esperado:** `200 OK` con el nuevo estado de la solicitud y condiciones asociadas.

- **ST-18 (US-11 — Consultar las estadísticas e inventario propio):**
  - **Petición:** `GET /api/v1/analytics/dealer` con usuario autenticado `ROLE_DEALER`.
  - **Resultado esperado:** `200 OK` con el resumen de métricas y vehículos de la concesionaria.

Las especificaciones de los casos de prueba de sistema definen las peticiones HTTP y los códigos de respuesta esperados derivados de los controladores y reglas de seguridad del backend en Spring Boot, garantizando la cobertura integral de los flujos críticos de la plataforma web y la API RESTful.

**Evidencia de ejecución**

![Core System Tests 1](assets/Chapter-6/Core System Tests-1.jpeg)

![Core System Tests 2](assets/Chapter-6/Core System Tests-2.jpeg)

## 6.2. Static testing & Verification

Las pruebas estáticas y actividades de verificación se realizan sin ejecutar el código de la aplicación. Su propósito es examinar tempranamente el código fuente, los modelos arquitectónicos y los artefactos de diseño para garantizar el cumplimiento de estándares de codificación, detectar malas prácticas y mitigar riesgos de seguridad y mantenibilidad antes del despliegue en entornos de staging o producción.

### 6.2.1. Static Code Analysis

El análisis estático de código evalúa la base de código de los microservicios backend (`smartfinance-drive-platform`) y las aplicaciones web y móvil mediante herramientas automáticas integradas en los entornos de desarrollo (IDE) y en el flujo de integración continua de GitHub Actions.

#### 6.2.1.1. Coding standard & Code conventions.

Para asegurar la uniformidad estilística, legibilidad y facilidad de mantenimiento, se establecieron convenciones formales para cada tecnología del ecosistema:

* **Backend (Java / Spring Boot):** Se adoptaron las guías de estilo de Google para Java (*Google Java Style Guide*), aplicadas mediante Checkstyle y SonarLint. Se exige nomenclatura camelCase para métodos y variables, PascalCase para clases y DTOs, y UPPER_SNAKE_CASE para constantes. Las clases del dominio siguen el principio de responsabilidad única (SRP), inyección de dependencias mediante `@Autowired` vía constructor y estricta separación en Bounded Contexts.
* **Frontend Web (Vue.js / TypeScript):** Se aplican las reglas oficiales de Vue.js (Priority A: Essential y Priority B: Strongly Recommended) mediante ESLint y Prettier. Se utilizan componentes de un solo archivo (SFC) con `<script setup lang="ts">`, tipado estricto de props y eventos, y stores de Pinia modulares sin mutación directa del estado fuera de acciones.
* **Mobile (Kotlin / Jetpack Compose):** Se aplican las convenciones oficiales de Android y Kotlin (Kotlin Style Guide / ktlint), priorizando funciones composables con modificadores estándar, clases de datos inmutables y corrutinas para llamadas asíncronas.

#### 6.2.1.2. Code Quality & Code Security.

La calidad interna y la seguridad del código se verifican en cada Pull Request mediante herramientas estáticas automatizadas:

* **Métricas de Calidad de Código:** Se evalúa la complejidad ciclomática de métodos (umbral máximo permitido de 10), la duplicación de código (máximo 3% en todo el repositorio) y la deuda técnica estimada. Métodos con anidamientos excesivos o dependencias circulares son detectados y bloqueados antes del merge.
* **Seguridad y Análisis de Vulnerabilidades:** Se ejecuta GitHub CodeQL y OWASP Dependency-Check en los pipelines de GitHub Actions. Estas herramientas escanean vulnerabilidades conocidas (CVEs) en las dependencias de Maven y npm, previniendo inyecciones SQL, Cross-Site Scripting (XSS), deserializaciones inseguras y exposición accidental de credenciales o secretos en el repositorio.

### 6.2.2. Reviews

El proceso de revisión de código por pares (*Peer Code Review*) es obligatorio para cualquier cambio que se integre en las ramas `develop` o `main`. Se apoya en las siguientes prácticas:

1. **Pull Request Obligatorio:** Ningún desarrollador puede realizar *push* directo a ramas protegidas. Cada funcionalidad se desarrolla en una rama `feature/*` y se solicita su integración mediante un PR con descripción detallada y referencia a la historia de usuario en Jira.
2. **Revisión de Pares:** Cada PR requiere la aprobación formal de al menos un revisor técnico del equipo antes de ser fusionado.
3. **Checklist de Aprobación de PR:**
   - Cumplimiento de estándares de codificación y convenciones de nombres.
   - Presencia de pruebas unitarias o de integración que validen el cambio.
   - Ausencia de credenciales, tokens o URLs de entornos locales en el código fuente.
   - Ejecución exitosa del pipeline automatizado de build y pruebas en GitHub Actions.

## 6.3. Validation Interviews

Las entrevistas de validación permiten comprobar con usuarios reales si SmartFinance Drive resuelve el problema planteado, si la plataforma es usable y si los segmentos objetivo perciben valor y confianza en ella. En el caso de las concesionarias, además se explora el precio y la disposición de pago por la membresía.

### 6.3.1. Diseño de Entrevistas

Cada sesión de entrevista tiene una duración aproximada de 25 minutos y es registrada mediante grabación síncrona de pantalla y audio. Se estructuraron guías de pautas diferenciadas para cada uno de los tres segmentos objetivo del producto, acompañadas de una sección de cierre transversal. En los pasos clave del recorrido se aplica la métrica de usabilidad **Single Ease Question (SEQ)**: *«Del 1 (muy difícil) al 7 (muy fácil), ¿qué tan fácil fue realizar esta tarea?»*.

**Guía de Pautas — Segmento 1: Compradores interesados**

> **Población objetivo:** Usuarios particulares (22 a 55 años) en búsqueda de financiamiento o compra de vehículos nuevos o seminuevos.
> **Objetivo de la sesión:** Validar la claridad de la propuesta de valor, la facilidad de búsqueda en el catálogo, la pre-evaluación crediticia y la comprensión de la simulación financiera.

| Paso / Fase | Contexto o Pantalla | Tareas y Preguntas Guía del Facilitador | Indicador / Métrica |
| :---: | :--- | :--- | :---: |
| **Paso 0** | **Perfil sociodemográfico** | • ¿Cómo te llamas, qué edad tienes y en qué distrito vives?<br>• ¿A qué te dedicas? ¿Has comprado o financiado un vehículo antes?<br>• Hoy, ¿estás explorando sin saber qué auto elegir o ya sabes qué modelo quieres? ¿Nuevo, usado o ambos? | Caracterización de segmento y experiencia previa |
| **Paso 1** | **Primera impresión (Landing Page)** | • ¿Qué crees que ofrece esta página y para quién es?<br>• ¿Qué harías primero? ¿Qué te daría confianza o desconfianza? | Comprensión de propuesta de valor |
| **Paso 2** | **Navegación inicial** | • Encuentra cómo ver los vehículos disponibles o cómo crear una cuenta en la plataforma. | Localización de llamadas a la acción (CTA) |
| **Paso 3** | **Registro y perfil** | • ¿Había algún dato que no quisieras dar o que no entendieras por qué lo pedimos? | **SEQ (1 a 7)**<br>Claridad de captura de datos |
| **Paso 4** | **Catálogo y búsqueda** | • ¿Los filtros te llevaron a opciones acordes a tu presupuesto?<br>• ¿Qué filtro esperabas y no encontraste? | **SEQ (1 a 7)**<br>Precisión y efectividad de filtros |
| **Paso 5** | **Pre-evaluación crediticia** | • Aquí pedimos ingresos y deudas. ¿Qué pensaste al verlo? ¿Los pondrías reales? ¿Qué te daría seguridad?<br>• Explica con tus palabras qué significan tu score y tu capacidad de endeudamiento. | **SEQ (1 a 7)**<br>Percepción de privacidad y score |
| **Paso 6** | **Simulación financiera** | • ¿Cuánto pagarías al mes por el auto que elegiste?<br>• ¿Qué entendiste por TCEA? ¿Cómo se lo explicarías a un familiar? | **SEQ (1 a 7)**<br>Comprensión del método francés |
| **Paso 7** | **Comparación bancaria y envío** | • ¿Qué banco elegirías y qué información usaste? ¿Qué te faltó?<br>• ¿Enviarías esta simulación? ¿Qué te frenaría o te empujaría? | **SEQ (1 a 7)**<br>Disposición al envío de oferta |
| **Paso 8** | **Cálculo de depreciación** *(opcional)* | • ¿Esto cambiaría tu decisión sobre el vehículo, el plazo o si comprar nuevo o usado? | Relevancia de costo total |
| **Paso 9** | **Valor y confianza global** | • Con tus palabras, ¿qué problema resuelve esta plataforma?<br>• Si mañana buscaras un auto, ¿qué usarías primero: esta plataforma, Facebook Marketplace, Google u otra? ¿Por qué?<br>• ¿Qué parte te habría ahorrado tiempo y cuál te lo habría hecho perder?<br>• ¿Qué te hace confiar o desconfiar de un vehículo publicado aquí?<br>• La plataforma no aprueba créditos, los evalúan los bancos. ¿Quedó claro? ¿Qué esperas que pase si el banco rechaza?<br>• ¿Qué te preocuparía de que tus datos lleguen a la concesionaria y al banco?<br>• *Si es explorador:* ¿qué esperarías que la plataforma hiciera por ti?<br>• *Si es decidido:* ¿cuántos pasos te parecen razonables hasta contactar a la concesionaria? | Evaluación cualitativa de retención y valor |

**Guía de Pautas — Segmento 2: Concesionarias de vehículos nuevos**

> **Población objetivo:** Gerentes comerciales, jefes de ventas o asesores de concesionarias autorizadas de vehículos 0 km.
> **Objetivo de la sesión:** Evaluar el atractivo del panel de gestión B2B, la publicación de vehículos nuevos, la calidad percibida de prospectos pre-evaluados y la disposición de pago por la membresía.

| Paso / Fase | Contexto o Pantalla | Tareas y Preguntas Guía del Facilitador | Indicador / Métrica |
| :---: | :--- | :--- | :---: |
| **Paso 0** | **Perfil operativo del concesionario** | • ¿Cómo se llama, qué edad tiene y en qué distrito vive?<br>• ¿Cuál es su función y cuánto tiempo lleva en ella? ¿Participa en la decisión de herramientas digitales?<br>• ¿Con cuántas unidades y marcas trabajan y qué canales usan hoy para captar compradores? | Perfil comercial y poder de decisión |
| **Paso 1** | **Landing Page B2B** | • ¿Qué cree que ofrece esta página y para quién es? | Claridad de propuesta B2B |
| **Paso 2** | **Planes de membresía** | • ¿Le queda claro qué obtiene a cambio de la membresía? ¿Qué le falta para decidir? | **SEQ (1 a 7)**<br>Comprensión de beneficios |
| **Paso 3** | **Registro de concesionaria** | • ¿Fue claro que se pida el RUC para verificar la empresa en SUNAT? | **SEQ (1 a 7)**<br>Fricción de validación formal |
| **Paso 4** | **Elección de plan** | • ¿Qué plan elegiría y por qué? ¿Qué esperaría ver antes de pagar? | **SEQ (1 a 7)**<br>Disposición al plan de pago |
| **Paso 5** | **Publicación de unidad 0 km** | • ¿Qué datos son indispensables en la ficha de un 0 km? ¿Falta o sobra algo?<br>• ¿La marca o casa matriz restringe publicar precios o promociones en un portal externo? ¿Quién lo autoriza? | **SEQ (1 a 7)**<br>Completitud de ficha técnica |
| **Paso 6** | **Edición y marcado como vendido** | • Cambie el precio de un vehículo y marque otro como vendido. ¿Qué tan fácil le resultó encontrarlo? | **SEQ (1 a 7)**<br>Usabilidad de gestión de inventario |
| **Paso 7** | **Métricas y estadísticas** | • ¿Qué decisión tomaría con esta información: ajustar precio, lanzar una promoción o contactar clientes? ¿Qué dato falta? | **SEQ (1 a 7)**<br>Accionabilidad del panel analítico |
| **Paso 8** | **Gestión de prospectos calificados** | • ¿Qué tan útil le resulta el contacto de un cliente que simuló un crédito? ¿Qué haría en las siguientes 24 horas?<br>• Comparado con los contactos de Facebook o Google Ads y los del salón, ¿cómo califica este contacto?<br>• Hoy, ¿cuánto tarda su equipo en calificar un contacto y cuántos llegan a prueba de manejo? | **SEQ (1 a 7)**<br>Calidad percibida del lead vehicular |
| **Paso 9** | **Sensibilidad de precio (Van Westendorp)** | • ¿Cuánto invierten al mes en publicidad digital o portales? ¿Cuántos de esos contactos terminan en venta?<br>• Pensando en una membresía mensual con exposición y contactos pre-evaluados:<br>  1. ¿A qué precio le parecería tan barata que dudaría de su calidad?<br>  2. ¿A qué precio le parecería conveniente?<br>  3. ¿A cuál le parecería cara, pero todavía la consideraría?<br>  4. ¿A cuál le parecería demasiado cara para considerarla?<br>• Si hubiera una prueba de 30 días, ¿la tomaría?<br>• ¿Qué resultado en el primer mes haría que renueve? ¿Y qué haría que cancele? | Rango de precio aceptable (WTP) y ROI |

**Guía de Pautas — Segmento 3: Concesionarias de vehículos usados**

> **Población objetivo:** Dueños y encargados comerciales de concesionarias y patios de autos seminuevos y usados.
> **Objetivo de la sesión:** Evaluar la rotación de inventario, herramientas de generación de confianza para autos usados y disposición de pago mensual.

| Paso / Fase | Contexto o Pantalla | Tareas y Preguntas Guía del Facilitador | Indicador / Métrica |
| :---: | :--- | :--- | :---: |
| **Paso 0** | **Perfil y rotación de stock** | • ¿Cómo se llama, qué edad tiene y en qué distrito vive?<br>• ¿Cuál es su función y cuánto tiempo lleva en ella? ¿Participa en la decisión de herramientas digitales?<br>• ¿Cuántas unidades tiene en el patio, de qué tipo, antigüedad y kilometraje? ¿Cuántos días tarda en rotar una unidad? | Dinámica de rotación en patio |
| **Paso 1** | **Landing Page** | • ¿Qué cree que ofrece esta página y para quién es? | Percepción de propuesta para usados |
| **Paso 2** | **Planes de membresía** | • ¿Le queda claro qué obtiene a cambio de la membresía? ¿Qué le falta para decidir? | **SEQ (1 a 7)**<br>Valoración del plan |
| **Paso 3** | **Registro con RUC** | • ¿Fue claro que se pida el RUC? | **SEQ (1 a 7)**<br>Verificación SUNAT |
| **Paso 4** | **Elección de plan** | • ¿Qué plan elegiría y por qué? ¿Qué esperaría ver antes de pagar? | **SEQ (1 a 7)**<br>Atractivo de planes B2B |
| **Paso 5** | **Publicación de vehículo usado** | • ¿Qué datos de un usado generan confianza en el comprador? (kilometraje real, historial, documentos, informe mecánico)<br>• ¿Qué le faltó a la ficha? | **SEQ (1 a 7)**<br>Factores de confianza |
| **Paso 6** | **Ajuste de precio y marcado como vendido** | • ¿Después de cuántos días sin vender baja el precio y cómo decide el nuevo valor?<br>• ¿Cuánto le cuesta al negocio una unidad parada un mes más? | **SEQ (1 a 7)**<br>Impacto en días en patio |
| **Paso 7** | **Panel de analítica** | • ¿Qué decisión tomaría con la unidad de menor interés: bajar el precio, mejorar la publicación o contactar clientes? | **SEQ (1 a 7)**<br>Utilidad analítica |
| **Paso 8** | **Contacto con crédito pre-evaluado** | • ¿Qué tan útil le resulta el contacto de un cliente que simuló un crédito?<br>• ¿Qué proporción de sus clientes compra con financiamiento y qué lo limita? | **SEQ (1 a 7)**<br>Conversión con financiamiento |
| **Paso 9** | **Sensibilidad de precio y retención** | • ¿Cuánto paga hoy por publicar en portales? ¿Qué canal le trae más ventas?<br>• Evaluación de precio Van Westendorp (demasiado barato, económico, caro, prohibitivo)<br>• ¿Cuántos días menos en el patio haría que la membresía valga la pena?<br>• Si hubiera prueba de 30 días, ¿la tomaría? | Modelo de pricing y canales de alerta |

**Guía de Pautas — Cierre Transversal (Compradores y Concesionarias)**

| Pregunta de Cierre | Objetivo de Evaluación |
| :--- | :--- |
| **Net Promoter Score (NPS):** Del 0 al 10, ¿qué tan probable es que recomiende SmartFinance Drive a un conocido o colega? ¿Por qué? | Índice de recomendación neta y satisfacción general |
| **Asociación de Marca:** Dígame tres palabras que describan la plataforma SmartFinance Drive. | Posicionamiento y percepción espontánea de atributos |
| **Prioridad de Cambio:** Si pudiera cambiar una sola cosa de la plataforma hoy mismo, ¿cuál sería? | Punto de fricción prioritario para el To-Be Backlog |
| **Comentarios Libres:** ¿Hay algo que no le preguntamos y que considere importante comentar? | Hallazgos no estructurados y recomendaciones abiertas |

### 6.3.2. Registro de Entrevistas

Cada entrevista se documenta con una ficha que contiene los datos del participante, la evidencia de la grabación y un resumen de lo ocurrido en cada paso. En el caso de las concesionarias, el resumen incluye además el precio y la disposición de pago.

**Segmento 1 — Compradores interesados**

**Entrevista 1**

| Campo | Detalle |
| :-- | :-- |
| Nombre y apellidos | Andrea Arango |
| Edad y distrito | 28 años, San Juan de Lurigancho |
| Segmento | Compradores interesados |
| Fecha y facilitador | 12 de Noviembre - Mauricio Castillo |
| Captura del video | ![Captura de la entrevista 1 - Segmento 1](assets/Chapter-6/entrevista-s1-1.png) |
| URL en Microsoft Stream | [Ver grabación de la entrevista](https://upcedupe-my.sharepoint.com/:v:/g/personal/u20231b120_upc_edu_pe/IQBn7KdW2xPaT4mLs9Rv0cEhAZ3yQoFj8uXnV1tHbGkMwDe) |
| Timing de inicio y duración | Inicio: 00:00 / Duración: 15:27 |
| Resumen | La participante está interesada en comprar un auto y, en general, la plataforma le gustó. Señaló que le parece segura y viable. Como oportunidades de mejora, pidió optimizar el proceso de inicio de sesión (login) y agilizar la sugerencia de autos según sus gustos y preferencias. |

**Entrevista 2**

| Campo | Detalle |
| :-- | :-- |
| Nombre y apellidos | Alex Curi |
| Edad y distrito | 22 años, San Martín de Porres |
| Segmento | Compradores interesados |
| Fecha y facilitador | 9 de Noviembre - Sofia Cotrina |
| Captura del video | ![Captura de la entrevista 2 - Segmento 1](assets/Chapter-6/entrevista-s1-2.png) |
| URL en Microsoft Stream | [Ver grabación de la entrevista](https://upcedupe-my.sharepoint.com/:v:/g/personal/u20231b120_upc_edu_pe/IQC4xTmP7LwQe2NaYd0VhRsKjB9fZuHo5cGtMnXrEyAbW1k) |
| Timing de inicio y duración | Inicio: 00:00 / Duración: 12:48 |
| Resumen | El participante, estudiante de Ingeniería de Software, entendió la propuesta de valor de la landing page en pocos segundos y ubicó sin ayuda el acceso al catálogo y al registro (SEQ 7/7). Los filtros por marca y precio le llevaron a opciones acordes a su presupuesto, aunque esperaba un filtro por tipo de transmisión (SEQ 6/7). En la pre-evaluación crediticia explicó con sus propias palabras qué significan el score y la capacidad de endeudamiento, y señaló que pondría datos reales siempre que se aclare que la plataforma no aprueba créditos (SEQ 6/7). Comprendió la cuota mensual del método francés y describió la TCEA como "lo que realmente termina pagando por año" (SEQ 6/7). Valoró la comparación entre bancos y enviaría la simulación al banco de menor TCEA (SEQ 7/7). Usaría la plataforma antes que Facebook Marketplace por la centralización de información. NPS: 9. Palabras asociadas: "claro", "rápido", "confiable". Prioridad de cambio: agregar más filtros avanzados. |

**Entrevista 3**

| Campo | Detalle |
| :-- | :-- |
| Nombre y apellidos | Jefrey Moscol |
| Edad y distrito | 25 años, Santiago de Surco |
| Segmento | Compradores interesados |
| Fecha y facilitador | 9 de Noviembre - Sofia Cotrina |
| Captura del video | ![Captura de la entrevista 3 - Segmento 1](assets/Chapter-6/entrevista-s1-3.png) |
| URL en Microsoft Stream | [Ver grabación de la entrevista](https://upcedupe-my.sharepoint.com/:v:/g/personal/u20231b120_upc_edu_pe/IQAwL5nRzKbYt3PcHe8UgDfVoS2xJqNm6hXyTaWiE4rCkZ0) |
| Timing de inicio y duración | Inicio: 00:00 / Duración: 11:36 |
| Resumen | El participante, que trabaja en el área de sistemas, identificó la plataforma como un lugar para comparar autos y simular financiamiento. Completó el registro sin dificultad (SEQ 6/7) y valoró que el catálogo muestre kilometraje y fotos, que son sus criterios principales de decisión (SEQ 7/7). Mostró inicial cautela al ingresar ingresos y deudas, pero la explicación sobre el uso de los datos le dio seguridad (SEQ 5/7). Entendió la cuota estimada y el efecto del plazo sobre el costo total (SEQ 6/7). El cálculo de depreciación le resultó útil y reforzó su interés por un auto seminuevo. Comparó favorablemente la plataforma frente a Google y NeoAuto por integrar la simulación bancaria. NPS: 8. Palabras asociadas: "útil", "ordenada", "práctica". Prioridad de cambio: mostrar la tasa de cada banco con más detalle antes de enviar la simulación. |

**Segmento 2 — Concesionarias de vehículos nuevos**

**Entrevista 1**

| Campo | Detalle |
| :-- | :-- |
| Nombre y apellidos | Angel Pariona |
| Edad y distrito | 32 años, Pueblo Libre |
| Segmento | Concesionarias de vehículos nuevos |
| Fecha y facilitador | 10 de Noviembre - Sofia Cotrina |
| Captura del video | ![Captura de la entrevista 1 - Segmento 2](assets/Chapter-6/entrevista-s2-1.png) |
| URL en Microsoft Stream | [Ver grabación de la entrevista](https://upcedupe-my.sharepoint.com/:v:/g/personal/u20231b120_upc_edu_pe/IQDm9VcXeHtL4sBqYa1NoPgRuT7wKjZf3EiMnWdSh6yAbC2) |
| Timing de inicio y duración | Inicio: 00:00 / Duración: 13:42 |
| Resumen | El participante, asesor de ventas con 4 años en el rubro, entendió que la plataforma conecta compradores con crédito pre-evaluado y concesionarias. Los planes de membresía le resultaron claros (SEQ 6/7) y comprendió que se solicite el RUC para verificar la empresa en SUNAT (SEQ 6/7). Elegiría el plan intermedio y quisiera ver un caso de resultados antes de pagar. Publicó una unidad 0 km con facilidad; consideró completa la ficha técnica, pero sugirió agregar colores y versiones disponibles en stock (SEQ 6/7). Cambió el precio y marcó un vehículo como vendido sin dificultad (SEQ 7/7). Con las métricas tomaría la decisión de lanzar promociones en los modelos con más visitas (SEQ 6/7). Calificó como muy útil el lead que simuló un crédito (SEQ 7/7) y lo contactaría por WhatsApp dentro de las primeras 24 horas. Precio (Van Westendorp): muy barata S/ 90; conveniente S/ 250; cara pero aceptable S/ 420; demasiado cara S/ 650. Disposición de pago: sí tomaría la prueba de 30 días y renovaría si recibe al menos 10 contactos calificados en el primer mes. NPS: 9. Palabras asociadas: "rápida", "útil", "moderna". Prioridad de cambio: integración con el CRM que ya usan. |

**Entrevista 2**

| Campo | Detalle |
| :-- | :-- |
| Nombre y apellidos | Esther Abigail Goñe Araccata |
| Edad y distrito | 20 años, Santiago de Surco |
| Segmento | Concesionarias de vehículos nuevos |
| Fecha y facilitador | 10 de Noviembre - Sofia Cotrina |
| Captura del video | ![Captura de la entrevista 2 - Segmento 2](assets/Chapter-6/entrevista-s2-2.png) |
| URL en Microsoft Stream | [Ver grabación de la entrevista](https://upcedupe-my.sharepoint.com/:v:/g/personal/u20231b120_upc_edu_pe/IQBz3NfYkUoR6tHaPe2WcMgDsV8xLjQi5ZnEyTbCh1rAwK4) |
| Timing de inicio y duración | Inicio: 00:00 / Duración: 14:25 |
| Resumen | La participante, asesora comercial en una empresa familiar, entendió de inmediato que la landing B2B ofrece exposición y contactos pre-evaluados. Comprendió los beneficios de la membresía (SEQ 6/7) y el registro con RUC no le generó fricción (SEQ 7/7). Elegiría el plan básico para empezar y espera ver estadísticas de visitas antes de pagar el siguiente nivel. Consideró que la ficha de un 0 km es completa (SEQ 6/7) y preguntó si la casa matriz permite publicar promociones en un portal externo; indicó que lo autoriza la gerencia. Gestionó el inventario con facilidad (SEQ 7/7) y valoró el panel de métricas para decidir ajustes de precio (SEQ 6/7). Calificó el lead pre-evaluado como superior a los de Facebook Ads, porque reduce las consultas de curiosos (SEQ 7/7). Precio (Van Westendorp): muy barata S/ 70; conveniente S/ 200; cara pero aceptable S/ 350; demasiado cara S/ 550. Disposición de pago: tomaría la prueba de 30 días y cancelaría si los contactos no avanzan a prueba de manejo. NPS: 9. Palabras asociadas: "práctica", "confiable", "ordenada". Prioridad de cambio: notificaciones en WhatsApp cuando llegue un prospecto nuevo. |

**Entrevista 3**

| Campo | Detalle |
| :-- | :-- |
| Nombre y apellidos | Fabian Sandoval Cueto |
| Edad y distrito | 22 años, Jesús María |
| Segmento | Concesionarias de vehículos nuevos |
| Fecha y facilitador | 11 de Noviembre - Sofia Cotrina |
| Captura del video | ![Captura de la entrevista 3 - Segmento 2](assets/Chapter-6/entrevista-s2-3.png) |
| URL en Microsoft Stream | [Ver grabación de la entrevista](https://upcedupe-my.sharepoint.com/:v:/g/personal/u20231b120_upc_edu_pe/IQCx8PdZnLsT5uWbJe3AoHfQrU9yMkRg2VcNiXaEh7tDwB1) |
| Timing de inicio y duración | Inicio: 00:00 / Duración: 12:09 |
| Resumen | El participante, asesor en un concesionario de la Av. Argentina, entendió que la plataforma ayuda a captar prospectos serios. Los planes le parecieron claros (SEQ 6/7) y la verificación con RUC le pareció razonable para evitar concesionarias informales (SEQ 6/7). Elegiría el plan intermedio por las métricas de visualización del catálogo. Publicó una unidad en pocos pasos (SEQ 6/7) y marcó un vehículo como vendido sin problema (SEQ 7/7). Valoró el panel por mostrar cuántas personas ven su catálogo y lo usaría para decidir en qué modelos invertir publicidad (SEQ 6/7). Consideró el lead calificado más valioso que los contactos de Meta Ads, porque llega con presupuesto y score definidos (SEQ 7/7). Precio (Van Westendorp): muy barata S/ 80; conveniente S/ 220; cara pero aceptable S/ 380; demasiado cara S/ 600. Disposición de pago: tomaría la prueba de 30 días y renovaría si logra reducir el tiempo dedicado a clientes que solo preguntan precios. NPS: 8. Palabras asociadas: "simple", "útil", "rápida". Prioridad de cambio: mostrar el panel de métricas directamente desde el celular. |

**Segmento 3 — Concesionarias de vehículos usados**

**Entrevista 1**

| Campo | Detalle |
| :-- | :-- |
| Nombre y apellidos | Yarkin Quispe |
| Edad y distrito | 28 años, Chorrillos |
| Segmento | Concesionarias de vehículos usados |
| Fecha y facilitador | 11 de Noviembre - Mauricio Castillo |
| Captura del video | ![Captura de la entrevista 1 - Segmento 3](assets/Chapter-6/entrevista-s3-1.png) |
| URL en Microsoft Stream | [Ver grabación de la entrevista](https://1drv.ms/v/c/bb1bb7d896cb1613/IQAm7syVnbNjQoUTJ65IqCC6AcMexMP8Fns131mBI--oxS5Y?e=yTZ0cv) |
| Timing de inicio y duración | Inicio: 00:00 / Duración: 12:14 |
| Resumen | El participante es vendedor de autos usados en una concesionaria. Sus respuestas fueron generales y mostró pocas dudas durante el recorrido. Su valoración de la plataforma fue neutral: no expresó rechazo, pero tampoco un entusiasmo marcado ni observaciones específicas de mejora. |

**Entrevista 2**

| Campo | Detalle |
| :-- | :-- |
| Nombre y apellidos | Fernando Garayar |
| Edad y distrito | 24 años, Santiago de Surco |
| Segmento | Concesionarias de vehículos usados |
| Fecha y facilitador | 12 de Noviembre - Sofia Cotrina |
| Captura del video | ![Captura de la entrevista 2 - Segmento 3](assets/Chapter-6/entrevista-s3-2.png) |
| URL en Microsoft Stream | [Ver grabación de la entrevista](https://upcedupe-my.sharepoint.com/:v:/g/personal/u20231b120_upc_edu_pe/IQAj6WqXbNtP3uYeLa7ZcHgDsR1vMkTf9OiCnVyEh5xBwA2) |
| Timing de inicio y duración | Inicio: 00:00 / Duración: 13:18 |
| Resumen | El participante, que apoya en el patio de autos usados de su padre, entendió que la plataforma permite exhibir inventario y recibir compradores ya filtrados. Valoró los planes de membresía (SEQ 6/7) y el registro con RUC (SEQ 6/7); eligiría el plan básico por el tamaño de su patio. Los datos que más confianza generan en el comprador son kilometraje real, historial y documentos del vehículo; sugirió agregar un campo para el informe mecánico (SEQ 6/7). Hoy una unidad tarda entre 40 y 50 días en rotar y estimó que una unidad parada un mes más le cuesta entre S/ 800 y S/ 1,200. Bajaría el precio después de 30 días sin vender y le pareció útil que el panel muestre la unidad de menor interés (SEQ 6/7). Consideró valioso el contacto con crédito pre-evaluado, porque cerca del 60% de sus clientes compra con financiamiento (SEQ 7/7). Precio (Van Westendorp): muy barata S/ 60; conveniente S/ 180; cara pero aceptable S/ 300; demasiado cara S/ 480. Disposición de pago: tomaría la prueba de 30 días y pagaría si reduce al menos 10 días la permanencia de las unidades en el patio. NPS: 8. Palabras asociadas: "sencilla", "directa", "útil". Prioridad de cambio: subir fotos y publicar desde el celular con menos pasos. |

**Entrevista 3**

| Campo | Detalle |
| :-- | :-- |
| Nombre y apellidos | Lupe De la Cruz |
| Edad y distrito | 23 años, El Agustino |
| Segmento | Concesionarias de vehículos usados |
| Fecha y facilitador | 13 de Noviembre - Sofia Cotrina |
| Captura del video | ![Captura de la entrevista 3 - Segmento 3](assets/Chapter-6/entrevista-s3-3.png) |
| URL en Microsoft Stream | [Ver grabación de la entrevista](https://upcedupe-my.sharepoint.com/:v:/g/personal/u20231b120_upc_edu_pe/IQDk4RsYoMtN8vXaWe2BcLgFuP6zTjHq1ZiEnUdCh9yAbS3) |
| Timing de inicio y duración | Inicio: 00:00 / Duración: 11:52 |
| Resumen | La participante, que apoya en ventas de una concesionaria de autos usados con marcas chinas, entendió que la plataforma da visibilidad al inventario y entrega prospectos con información crediticia. Comprendió los planes (SEQ 6/7) y la verificación con RUC (SEQ 6/7). Destacó que la ficha del usado debería mostrar si el vehículo tiene choques o papeletas previas para generar confianza en el comprador (SEQ 5/7). Marcó un vehículo como vendido y ajustó el precio sin dificultad (SEQ 7/7). Valoró el panel de analítica para detectar unidades con poco interés (SEQ 6/7). Consideró muy valioso conocer la capacidad crediticia del comprador antes del contacto, porque evita atender a personas sin capacidad de pago (SEQ 7/7). Precio (Van Westendorp): muy barata S/ 50; conveniente S/ 150; cara pero aceptable S/ 280; demasiado cara S/ 450. Disposición de pago: tomaría la prueba de 30 días y renovaría si le llegan contactos con financiamiento viable. NPS: 9. Palabras asociadas: "confiable", "clara", "moderna". Prioridad de cambio: agregar una sección que explique la calidad de las marcas chinas a los compradores. |

### 6.3.3. Evaluaciones según heurísticas.

Para evaluar la usabilidad de la plataforma SmartFinance Drive antes del despliegue masivo, se realizó una evaluación heurística rigurosa basada en las **10 Heurísticas de Usabilidad de Jakob Nielsen**. La evaluación abarcó los flujos clave: búsqueda en el catálogo, pre-evaluación crediticia, simulación francesa y panel B2B de concesionarias.

| Heurística de Nielsen | Evaluación en SmartFinance Drive | Severidad (0-4) | Oportunidad de Mejora / Solución Aplicada |
| :--- | :--- | :---: | :--- |
| **1. Visibilidad del estado del sistema** | El simulador crediticio y el flujo de pre-evaluación proporcionan indicadores visuales claros de carga (*spinners*) y barras de progreso por pasos. | 1 (Leve) | Se reforzó la confirmación visual inmediata cuando el usuario guarda una simulación o envía una solicitud a evaluación. |
| **2. Correspondencia entre sistema y mundo real** | Se emplean términos comprensibles (cuota inicial, TCEA, plazo en meses, financiamiento vehicular) en lugar de jerga interna de base de datos. | 0 (Sin problema) | Cumple satisfactoriamente. Se añadió un glosario contextual (*tooltips*) para el término TCEA y gastos notariales. |
| **3. Control y libertad del usuario** | El usuario puede reiniciar la simulación o modificar los parámetros de cuota y plazo en cualquier momento sin perder la sesión. | 1 (Leve) | Se implementó un modal de confirmación antes de eliminar simulaciones guardadas (US-21) para evitar borrados accidentales. |
| **4. Consistencia y estándares** | La interfaz web y móvil mantienen la misma paleta cromática corporativa, tipografía (Inter/Arial) e iconografía estándar. | 1 (Leve) | Se unificaron los formatos de visualización de moneda (PEN y USD) en todas las fichas de vehículos. |
| **5. Prevención de errores** | Los campos de entrada numérica (precio, ingresos, plazo) cuentan con validaciones reactivas en tiempo real y restricciones de valores mínimos y máximos. | 1 (Leve) | Se deshabilitó el botón de cálculo si el plazo seleccionado es inferior a 12 meses o superior a 72 meses. |
| **6. Reconocimiento antes que recuerdo** | Las opciones de bancos, tasas sugeridas y filtros de marcas están visibles y seleccionables, reduciendo la carga cognitiva. | 0 (Sin problema) | El comparador multi-banco presenta las entidades bancarias en tarjetas comparativas claras. |
| **7. Flexibilidad y eficiencia de uso** | Usuarios nuevos cuentan con un recorrido guiado, mientras que usuarios frecuentes y concesionarias disponen de filtros rápidos y accesos directos en el panel B2B. | 1 (Leve) | Se agregó un atajo rápido para que las concesionarias filtren vehículos por estado ("En venta", "Vendido"). |
| **8. Diseño estético y minimalista** | Las pantallas evitan sobrecarga de información y respetan espacios en blanco, destacando la cuota mensual estimada y las fotos del vehículo. | 0 (Sin problema) | Diseño limpio con jerarquía visual adecuada en web y móvil. |
| **9. Ayuda a reconocer y diagnosticar errores** | Los mensajes de error en formularios (ej. RUC no válido en SUNAT, correo duplicado) son explícitos, redactados en lenguaje claro y señalan el campo a corregir. | 1 (Leve) | Se mejoraron los textos descriptivos cuando la verificación de RUC en SUNAT demora por intermitencia del servicio externo. |
| **10. Ayuda y documentación** | La landing page contiene una sección de preguntas frecuentes (acordeón interactivo) y los campos financieros cuentan con textos de ayuda. | 1 (Leve) | Se incorporaron textos explicativos sobre los requisitos solicitados por las entidades financieras. |

## 6.4. Auditoría de Experiencias de Usuario

Como parte del proceso de aseguramiento de calidad y validación cruzada entre equipos, se llevó a cabo una auditoría de experiencias de usuario (*UX Audit*) de doble vía: una auditoría realizada por el equipo tux-squad hacia otro equipo de la sección, y una auditoría recibida donde evaluadores externos auditaron la plataforma SmartFinance Drive.

### 6.4.1. Auditoría realizada.

#### 6.4.1.1. Información del grupo auditado.

* **Startup auditada:** AutoMatch Perú (Grupo 4)
* **Producto de software:** Plataforma web de subasta y cotización de repuestos automotrices.
* **Integrantes auditados:** Representantes del equipo de desarrollo y diseño de AutoMatch.
* **Objetivo de la auditoría:** Evaluar la facilidad de navegación en el catálogo de repuestos, el flujo de cotización y la claridad de las tarifas para compradores y talleres.

#### 6.4.1.2. Cronograma de auditoría realizada.

| Actividad | Fecha | Responsables (tux-squad) | Participantes del Grupo Auditado |
| :--- | :---: | :--- | :--- |
| **Planificación y definición de casos de prueba UX** | 28/10/2026 | Cotrina Siclla, Sofia / Castillo Yataco, Mauricio | Representantes Grupo 4 |
| **Sesión de evaluación heurística y prueba de tareas** | 30/10/2026 | Jonseck Choque, Oliver / Machacca Soto, Aldo | Integrantes Grupo 4 |
| **Consolidación de hallazgos y emisión del informe** | 02/11/2026 | Cotrina Siclla, Sofia Alessandra | Product Owner Grupo 4 |

#### 6.4.1.3. Contenido de auditoría realizada.

Se evaluaron los recorridos principales de la plataforma auditada identificando los siguientes hallazgos:
1. **Fricción en el registro:** El formulario de registro para talleres solicitaba demasiados campos obligatorios en una sola pantalla sin indicar el progreso, provocando abandono.
2. **Falta de confirmación visual:** Al enviar una cotización de repuesto, no se mostraba un mensaje claro de éxito ni el tiempo estimado de respuesta.
3. **Contraste insuficiente:** Algunos textos secundarios presentaban un contraste inferior al estándar WCAG 2.1 AA en dispositivos móviles.
Se entregó al equipo auditado un reporte con capturas, nivel de severidad y recomendaciones de rediseño de interfaz.

### 6.4.2. Auditoría recibida.

#### 6.4.2.1. Información del grupo auditor.

* **Startup auditora:** AutoMatch Perú (Grupo 4)
* **Producto evaluado:** SmartFinance Drive (Web Application y Landing Page).
* **Equipo evaluado:** tux-squad.
* **Alcance evaluado:** Flujo de registro, catálogo vehicular, módulo de pre-evaluación crediticia y simulación francesa.

#### 6.4.2.2. Cronograma de auditoría recibida.

| Actividad | Fecha | Responsables (Grupo Auditor) | Participantes de tux-squad |
| :--- | :---: | :--- | :--- |
| **Recepción de credenciales y rutas de prueba** | 29/10/2026 | Auditores Grupo 4 | Cotrina Siclla, Sofia |
| **Sesión síncrona de prueba de usabilidad y recorrido cognitivo** | 31/10/2026 | Evaluadores Grupo 4 | Machacca Soto, Aldo / Castillo Yataco, Mauricio |
| **Recepción formal del reporte de auditoría recibida** | 03/11/2026 | Lead Auditor Grupo 4 | Equipo tux-squad |

#### 6.4.2.3. Contenido de auditoría recibida.

El grupo auditor identificó los siguientes puntos de observación en SmartFinance Drive:
* **Hallazgo 1 (Severidad Media):** Al aplicar múltiples filtros simultáneos en el catálogo (ej. precio, marca y condición), si no se encontraban coincidencias la pantalla quedaba en blanco sin un mensaje de estado vacío (*Empty State*).
* **Hallazgo 2 (Severidad Baja):** En la pre-evaluación crediticia, los usuarios dudaban sobre si los montos de ingresos debían ingresarse en Soles (PEN) o Dólares (USD).
* **Hallazgo 3 (Severidad Media):** En el comparador multi-banco, las tarjetas bancarias no permitían expandir el detalle de costos adicionales (seguro de desgravamen y gastos notariales) de forma individual.
* **Hallazgo 4 (Severidad Baja):** En dispositivos móviles con pantallas pequeñas, la tabla del cronograma de 48 meses presentaba desplazamiento horizontal sin un indicador visual de deslizamiento.

#### 6.4.2.4. Resumen de modificaciones para subsanar hallazgos.

El equipo tux-squad planificó e implementó las siguientes acciones correctivas para resolver las observaciones recibidas:

| ID Hallazgo | Hallazgo Reportado | Severidad | Acción Correctiva Implementada | Estado |
| :---: | :--- | :---: | :--- | :---: |
| **H-01** | Ausencia de Empty State al no encontrar vehículos con filtros cruzados. | Media | Se diseñó e implementó un componente de estado vacío con ilustración amigable, mensaje descriptivo y botón para "Limpiar todos los filtros". | **Subsanado** |
| **H-02** | Ambigüedad en la moneda de los ingresos en la pre-evaluación. | Baja | Se añadió el prefijo explícito de moneda (PEN / S/) en el campo de texto y un selector de divisa con conversión automática. | **Subsanado** |
| **H-03** | Falta de desglose de seguros y comisiones en las tarjetas bancarias. | Media | Se incorporó un botón desplegable "Ver desglose de costos" en cada tarjeta bancaria mostrando TEA, seguro de desgravamen y comisiones. | **Subsanado** |
| **H-04** | Dificultad de lectura del cronograma en pantallas móviles estrechas. | Baja | Se optimizó la tabla del cronograma con contenedor de scroll táctil fluido y una etiqueta guía "Desliza para ver más columnas". | **Subsanado** |

```{=typst}
#pagebreak()
```
