# Arquitectura prevista

El backend utilizará Go y Clean Architecture, con PostgreSQL como persistencia y HTTP como entrada. Esta estructura define responsabilidades futuras; todavía no implementa entidades, casos de uso, interfaces ni conexiones.

## Responsabilidades

| Ubicación | Responsabilidad prevista |
| --- | --- |
| `backend/internal/domain/` | Entidades y reglas de negocio independientes de HTTP, PostgreSQL y frameworks. |
| `backend/internal/application/` | Casos de uso que coordinan el dominio y definen las interfaces que necesitan para acceder a servicios externos. |
| `backend/internal/adapters/http/` | Traducción de solicitudes HTTP a entradas de casos de uso y de sus resultados a respuestas HTTP. |
| `backend/internal/adapters/postgres/` | Implementaciones de las interfaces de persistencia requeridas por la aplicación; SQL y traducción entre registros y modelos del dominio. |
| `backend/internal/platform/` | Configuración técnica y gestión de conexiones y otros recursos de infraestructura. |
| `backend/cmd/api/` | Punto de composición: construye las dependencias concretas, las conecta con los casos de uso y arranca el servidor. |
| `backend/migrations/` | Futuras migraciones versionadas del esquema PostgreSQL. |
| `frontend/src/app/` | Interfaz Next.js con App Router; consumirá la API cuando exista. |

## Dirección de las dependencias

Las dependencias de código apuntan hacia el interior:

```text
adapters/http ───────> application ───────> domain
adapters/postgres ──> application / domain
cmd/api ───────────> application + adapters + platform
```

El dominio no importa la aplicación ni la infraestructura. La aplicación conoce el dominio y los contratos que requiere, pero no implementaciones HTTP o PostgreSQL. Los adaptadores dependen de esos contratos; el punto de composición proporciona las implementaciones concretas.

Por ejemplo, un futuro caso de uso podrá requerir persistencia mediante una interfaz definida junto a quien la consume. El adaptador PostgreSQL implementará ese contrato. Así, un cambio de transporte o almacenamiento no obliga a modificar las reglas de negocio. La configuración y las conexiones pertenecen a infraestructura y no deben introducir dependencias de `platform` en el dominio o los casos de uso.

## Implementación incremental

Las entidades y reglas concretas se definirán a partir de requisitos validados de gestión de trading multiusuario. Los contratos se introducirán cuando un caso de uso real los necesite: no se crean interfaces vacías, repositorios genéricos ni abstracciones anticipadas.

La inicialización del módulo Go queda pendiente de la URL definitiva del repositorio o de una ruta de módulo oficial. No hay aún servidor, autenticación, conexión a PostgreSQL ni lógica de negocio.
