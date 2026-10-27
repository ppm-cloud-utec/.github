# Portafolio — SaaS de Project Portfolio Management

Proyecto Final de **CS2032 Cloud Computing** (UTEC, ciclo 2026-2) · **Grupo 4**

Solución SaaS **multi-tenant, serverless y basada en eventos** en AWS para
gestionar portafolios, proyectos, tareas, recursos, presupuestos y prioridades.

## Repositorios

| Repo | Responsable | Base de datos | Qué hace |
|---|---|---|---|
| [infra-compartida](../../../infra-compartida) | Osomar1705 | — | RDS, SNS, S3, authorizer, idempotencia |
| [ms-identidad](../../../ms-identidad) | Osomar1705 | DynamoDB | tenants, usuarios, login, JWT |
| [ms-portafolios](../../../ms-portafolios) | Brisseth-raton | RDS | portafolios, proyectos, admisión, prioridad |
| [ms-tareas](../../../ms-tareas) | fabianbot1331 | DynamoDB | tareas, hitos, dependencias |
| [ms-recursos](../../../ms-recursos) | sebastianperez72 | RDS | personas, capacidad, asignaciones |
| [ms-presupuestos](../../../ms-presupuestos) | carloscondor1610 | RDS | presupuesto, gastos, ejecución |
| [ms-analitico](../../../ms-analitico) | Osomar1705 | S3 + Athena | data lake, KPIs del portafolio |
| [web-ppm](../../../web-ppm) | alxgr-08 | — | Next.js en Amplify |

## Documentación

Vive en [infra-compartida/docs](../../../infra-compartida/tree/main/docs):
propuesta funcional, arquitectura, modelo de eventos, convenciones, reparto y
cronograma.

## Orden de despliegue

```
infra-compartida  →  ms-identidad  →  los otros 5 (en paralelo)  →  web-ppm
```

`infra-compartida` es bloqueante: de ahí salen el topic SNS, el authorizer y el
endpoint del RDS que todos importan.

## Los 3 tenants

| tenant_id | Organización | Perfil |
|---|---|---|
| `t-acme` | Acme Ingeniería | obras grandes, pocas tareas, mucho presupuesto |
| `t-globex` | Globex Consulting | consultorías cortas, recursos compartidos |
| `t-initech` | Initech Software | desarrollos largos, muchas tareas |

30,000 registros ficticios por microservicio, repartidos entre los 3.
