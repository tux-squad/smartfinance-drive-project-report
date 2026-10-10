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

#### Pruebas por contexto

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

#### Ejemplos de pruebas

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

#### Ejecución de las pruebas

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

#### Pruebas de controladores core

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

#### Pruebas de integración HTTP con MockMvc

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

#### Ejecución de las pruebas de integración

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

#### Configuración

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

#### Relación entre features y User Stories

| Feature | Archivo | Escenarios | Bounded context | User Story |
| --- | --- | ---: | --- | --- |
| Registro de usuario | `user-registration.feature` | 3 | IAM | US-01 Registro de cuenta y perfil personal (escenario 2: datos inválidos) |
| Publicación de vehículos en el catálogo | `vehicle-listing.feature` | 4 | Catalog | US-16 Publicar vehículo (escenarios 1 y 2: publicación exitosa y con datos inválidos) |
| Generación del plan de financiamiento | `financing-plan.feature` | 3 | Financing | US-29 Crear simulación de crédito vehicular; US-30 Ver cronograma detallado de pagos |
| Evaluación de riesgo crediticio | `credit-scoring.feature` | 4 | Scoring | US-28 Pre-evaluación de riesgo crediticio |
| Ciclo de vida de la solicitud de crédito | `credit-application.feature` | 5 | Financing | US-36 Evaluación oficial de solicitud de crédito |

#### Feature 1: Generación del plan de financiamiento

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

#### Feature 2: Evaluación de riesgo crediticio

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

#### Feature 3: Registro de usuario

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

#### Feature 4: Publicación de vehículos en el catálogo

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

#### Feature 5: Ciclo de vida de la solicitud de crédito

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

#### Ejecución de los escenarios BDD

```bash
./mvnw test -Dtest=CucumberSuiteTest
```

| Alcance ejecutado | Escenarios | Exitosos | Fallidos | Omitidos |
| --- | ---: | ---: | ---: | ---: |
| 5 features (IAM, Catalog, Financing, Scoring) | 19 | 19 | 0 | 0 |

![Figura 6.3](assets/Chapter-6/figura-6-3.png)

### 6.1.4. Core System Tests

Las pruebas de sistema validan la aplicación **completa y en ejecución** (API REST, Spring Security, JWT y base de datos PostgreSQL), recorriendo los flujos de usuario de extremo a extremo a través de la API documentada con OpenAPI/Swagger. A diferencia de las pruebas anteriores, aquí no se simula ningún componente interno.

#### Entorno de ejecución

| Elemento | Valor |
| --- | --- |
| Aplicación | `smartfinance-drive-platform` ejecutándose localmente (`./mvnw spring-boot:run`) |
| Base de datos | PostgreSQL con migraciones Flyway aplicadas al arrancar |
| URL base | `http://localhost:8080` |
| Herramienta cliente | Swagger UI (`/swagger-ui/index.html`) o Postman |
| Autenticación | `Authorization: Bearer <token>` obtenido en `POST /api/v1/auth/sessions` |

#### Casos de prueba de sistema

| ID | User Story | Caso de prueba | Petición | Resultado esperado | Resultado obtenido |
| --- | --- | --- | --- | --- | --- |
| ST-01 | US-01 | Registro exitoso | `POST /api/v1/auth/registrations` con correo, contraseña y datos válidos | `201 Created` | Pendiente de ejecutar |
| ST-02 | US-01 | Registro con datos inválidos | `POST /api/v1/auth/registrations` con un correo mal formado | `400 Bad Request` | Pendiente de ejecutar |
| ST-03 | US-02 | Inicio de sesión exitoso | `POST /api/v1/auth/sessions` con las credenciales registradas | `200 OK` con `token` y `refreshToken` | Pendiente de ejecutar |
| ST-04 | US-03 | Cierre de sesión | `DELETE /api/v1/auth/sessions/current` con `Authorization: Bearer <token>` | `200 OK` con el mensaje `User signed out successfully` | Pendiente de ejecutar |
| ST-05 | US-03 | Uso de la sesión anterior tras cerrar sesión | Cualquier endpoint protegido con el mismo token ya cerrado | Acceso rechazado (`401 Unauthorized`) | Pendiente de ejecutar |
| ST-06 | US-08 | Modificar roles como administrador | `PUT /api/v1/users/{userId}/roles` con un usuario `ROLE_ADMIN` | `200 OK` con los roles actualizados | Pendiente de ejecutar |
| ST-07 | US-08 | Modificar roles sin ser administrador | `PUT /api/v1/users/{userId}/roles` con un usuario `ROLE_USER` | `403 Forbidden` | Pendiente de ejecutar |
| ST-08 | US-16 | Publicar un vehículo como concesionaria | `POST /api/v1/vehicles` con un usuario `ROLE_DEALER` y datos válidos | `201 Created` con el vehículo creado | Pendiente de ejecutar |
| ST-09 | US-16 | Publicar un vehículo con datos inválidos | `POST /api/v1/vehicles` con año de fabricación 1899 | `400 Bad Request` y el vehículo no se registra | Pendiente de ejecutar |
| ST-10 | US-23 | Buscar vehículos con filtros | `GET /api/v1/vehicles?brand=Toyota&minPrice=10000&maxPrice=30000&condition=NEW` | `200 OK` con la lista paginada que cumple los filtros | Pendiente de ejecutar |
| ST-11 | US-25 | Ver el detalle de un vehículo | `GET /api/v1/vehicles/{vehicleId}` | `200 OK` con los datos del vehículo | Pendiente de ejecutar |
| ST-12 | US-18 | Cambiar el estado de un vehículo ajeno | `PATCH /api/v1/vehicles/{vehicleId}/status` con una concesionaria que no es la propietaria | `403 Forbidden` (regla `isVehicleOwner`) | Pendiente de ejecutar |
| ST-13 | US-28 | Pre-evaluación de riesgo crediticio | `POST /api/v1/credit-scores` con ingreso 5 000 PEN y cuota 1 200 PEN | `201 Created` con `riskTier = TIER_A` | Pendiente de ejecutar |
| ST-14 | US-29 | Crear una simulación de crédito | `POST /api/v1/simulations` con precio 25 000 USD, cuota inicial 20 % y 24 meses | `201 Created`; el cronograma incluye 24 pagos (US-30) | Pendiente de ejecutar |
| ST-15 | US-32 | Eliminar la simulación de otro cliente | `DELETE /api/v1/simulations/{id}` con un token distinto al del propietario | `403 Forbidden` (regla `isSimulationOwner`) | Pendiente de ejecutar |
| ST-16 | US-36 | Evaluar una solicitud sin ser entidad financiera | `PATCH /api/v1/credit-applications/{id}/status` con un usuario `ROLE_USER` | `403 Forbidden` | Pendiente de ejecutar |
| ST-17 | US-36 | Registrar la evaluación como entidad financiera | `PATCH /api/v1/credit-applications/{id}/status` con un usuario `ROLE_FINANCIAL_INSTITUTION` | `200 OK` con el nuevo estado de la solicitud | Pendiente de ejecutar |
| ST-18 | US-21 | Consultar las estadísticas propias | `GET /api/v1/analytics/dealer` con un usuario `ROLE_DEALER` | `200 OK` con las métricas de la concesionaria | Pendiente de ejecutar |

Las historias de la aplicación móvil (US-38 a US-45) y las de interfaz exclusivamente visual se validan en sus propios clientes. Los códigos esperados se derivaron de las reglas de seguridad y de los controladores del backend; si al ejecutar un caso el código obtenido difiere, debe registrarse el obtenido y analizarse la causa.

#### Evidencia de ejecución

![Core System Tests 1](assets/Chapter-6/Core System Tests-1.jpeg)

![Core System Tests 2](assets/Chapter-6/Core System Tests-2.jpeg)
