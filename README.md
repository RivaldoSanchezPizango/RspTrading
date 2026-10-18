# rspTrading

Plataforma multiusuario de gestión de trading activo. La arquitectura prevista combina un frontend Next.js con un backend Go basado en Clean Architecture y PostgreSQL.

**Estado actual:** estructura inicial y página mínima generada por Next.js. La funcionalidad del backend, las pantallas de negocio, la autenticación y la base de datos están pendientes.

## Iniciar el frontend

Desde la raíz del proyecto, en PowerShell:

```powershell
cd frontend
npm ci
npm run dev
```

Abrir <http://localhost:3000>. Para validar y ejecutar la compilación de producción desde `frontend/`:

```powershell
npm run lint
npm run build
npm run start
```

El lint ejecuta ESLint directamente; la compilación de Next.js no lo sustituye.

## Requisitos y versiones

Se requiere Node.js **20.9.0 o superior** y npm. Entorno utilizado: Windows, PowerShell 5.1, Node.js **24.16.0** y npm **11.13.0**.

| Dependencia instalada | Versión |
| --- | --- |
| Next.js / eslint-config-next | 16.4.2 |
| React / React DOM | 19.3.0 |
| TypeScript | 5.9.3 |
| Tailwind CSS / @tailwindcss/turbopack | 4.3.3 |
| ESLint | 9.39.5 |

`frontend/package-lock.json` conserva las versiones resueltas. El frontend utiliza App Router, TypeScript, ESLint, Tailwind CSS, `src/` y el alias `@/*`.

Go y PostgreSQL son tecnologías previstas: todavía no se fijaron sus versiones ni se requieren para ejecutar este scaffold. **La inicialización de `go.mod` queda diferida hasta conocer la URL definitiva del repositorio o la ruta oficial del módulo.**

## Estructura

```text
rspTrading/
├── frontend/
│   ├── src/app/
│   ├── package.json
│   └── package-lock.json
├── backend/
│   ├── cmd/api/
│   ├── internal/
│   │   ├── domain/
│   │   ├── application/
│   │   ├── adapters/
│   │   │   ├── http/
│   │   │   └── postgres/
│   │   └── platform/
│   └── migrations/
└── docs/
    └── architecture.md
```

Las carpetas vacías del backend contienen únicamente `.gitkeep`. Existe un único repositorio Git en la raíz. Los archivos `.env` y sus variantes están ignorados a cualquier profundidad, salvo `.env.example`; los ejemplos futuros deben contener solo valores ficticios.

## Arquitectura y siguiente paso

Ver [responsabilidades y dependencias](docs/architecture.md). Antes de implementar el backend se deben definir la ruta del módulo y los primeros casos de uso; este scaffold no incluye código Go, interfaces vacías ni migraciones ejecutables.
