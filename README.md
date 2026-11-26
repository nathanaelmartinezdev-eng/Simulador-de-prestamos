         # API de Préstamos (Simulador de Créditos)

API REST para simular, solicitar, aprobar y dar seguimiento a créditos personales. El proyecto se construye desde cero como práctica de Java y Spring Boot, con reglas de negocio inspiradas en el sector bancario.

## Objetivos

- Modelar un dominio financiero con reglas claras y verificables.
- Calcular tablas de amortización con precisión monetaria (`BigDecimal`).
- Garantizar que los pagos se registren de forma atómica.
- Probar la lógica de negocio con pruebas unitarias y de integración.

## Alcance

### Incluye (versión 1.0)

- Registro de clientes.
- Simulación de crédito: monto, plazo y tasa anual, con cálculo de cuota mensual.
- Solicitud de crédito por cliente.
- Aprobación o rechazo de la solicitud.
- Generación de la tabla de amortización al aprobar un crédito.
- Registro de pagos que reducen el saldo.
- Consulta del estado de un crédito y su historial de pagos.

### No incluye (por ahora)

- Autenticación y autorización (se considera en una versión posterior).
- Integración con sistemas bancarios reales o pasarelas de pago.
- Interfaz gráfica; el proyecto es solo API.
- Cálculo de intereses moratorios y penalizaciones.
- Múltiples monedas.

## Entidades

| Entidad | Descripción |
|---|---|
| `Cliente` | Persona que solicita créditos. |
| `Solicitud` | Petición de crédito de un cliente, con monto, plazo y tasa. |
| `Credito` | Crédito aprobado, con su tabla de amortización y saldo. |
| `Pago` | Abono que se aplica al saldo de un crédito. |

## Estados

**Solicitud:** `PENDIENTE` → `APROBADA` o `RECHAZADA`

**Crédito:** `ACTIVO` → `LIQUIDADO`

Las transiciones inválidas deben rechazarse con una excepción de negocio.

## Reglas de negocio

1. El monto solicitado debe ser mayor a cero y menor o igual al límite configurado.
2. El plazo debe estar entre 1 y 60 meses.
3. La tasa anual debe ser mayor o igual a cero.
4. Una solicitud solo puede aprobarse o rechazarse si está `PENDIENTE`.
5. Un pago no puede exceder el saldo pendiente del crédito.
6. Un crédito pasa a `LIQUIDADO` cuando su saldo llega a cero.
7. Los montos monetarios se manejan con `BigDecimal`, nunca con `double`.

*Ajusta los valores de los límites (monto máximo, plazo y tasa) según lo que quieras practicar.*

## Endpoints previstos

| Método | Ruta | Descripción |
|---|---|---|
| `POST` | `/clientes` | Registrar cliente |
| `GET` | `/clientes/{id}` | Consultar cliente |
| `POST` | `/solicitudes` | Crear solicitud de crédito |
| `PATCH` | `/solicitudes/{id}/aprobar` | Aprobar solicitud |
| `PATCH` | `/solicitudes/{id}/rechazar` | Rechazar solicitud |
| `GET` | `/creditos/{id}` | Consultar crédito y saldo |
| `POST` | `/creditos/{id}/pagos` | Registrar pago |

## Stack

- Java 17
- Spring Boot 3.x
- Spring Data JPA y Hibernate
- H2 (desarrollo) y PostgreSQL (pruebas y ejecución con Docker)
- JUnit 5, Mockito y Testcontainers
- Docker y Docker Compose

## Cómo ejecutarlo

*Se completará en la semana 14.*

## Decisiones de diseño

*Se irán documentando conforme avance el proyecto. Ejemplos de lo que debes explicar: por qué `BigDecimal`, cómo modelaste los estados y qué dejaste fuera del alcance y por qué.*

## Roadmap

Ver el plan de 15 semanas en el documento de roadmap.