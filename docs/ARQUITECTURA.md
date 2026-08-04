# Arquitectura del Ecosistema Digital Terrae

## 1. Visión general

Terrae es un ecosistema compuesto por cuatro dominios técnicos que se
desarrollarán de forma incremental sobre la base visual y funcional ya
validada en el simulador (`frontend/simulator/index.html`):

```
┌─────────────────────────────────────────────────────────────────┐
│                        USUARIOS FINALES                          │
│   Clientes · Joyeros · Auditores · Administradores Terrae         │
└───────────────────────────────┬───────────────────────────────────┘
                                 │
                    ┌────────────▼────────────┐
                    │        FRONTEND          │
                    │  React + Next.js + TS     │
                    │  (migrado desde simulador) │
                    └────────────┬────────────┘
                                 │ REST (JSON) / JWT
                    ┌────────────▼────────────┐
                    │         BACKEND           │
                    │   FastAPI (Python)         │
                    │   Clean Architecture        │
                    │   Repository Pattern        │
                    └───┬─────────┬──────────┬───┘
                        │         │          │
           ┌────────────▼──┐ ┌────▼─────┐ ┌──▼─────────────┐
           │  PostgreSQL     │ │ SIEGEM Lab│ │  EmeraldChain   │
           │  (SQLAlchemy)    │ │ IA (PyTorch│ │  Blockchain     │
           │  Datos estructu- │ │ OpenCV,    │ │  Polygon/       │
           │  rados del        │ │ YOLO)      │ │  Solidity       │
           │  negocio          │ │            │ │                 │
           └──────────────────┘ └────────────┘ └─────────────────┘
```

## 2. Principios arquitectónicos

- **Clean Architecture / DDD**: separación estricta entre dominio, casos de
  uso, infraestructura y presentación. El dominio no depende de frameworks.
- **Repository Pattern**: toda persistencia se accede vía interfaces de
  repositorio, permitiendo cambiar de almacenamiento (JSON → PostgreSQL) sin
  tocar la lógica de negocio.
- **Service Layer**: la lógica de negocio vive en servicios, no en los
  controladores/endpoints.
- **DTOs y validación**: entrada y salida de la API validadas con Pydantic;
  nunca se exponen directamente los modelos de dominio.
- **Gateway de Blockchain simulable**: un `BlockchainGateway` con
  implementación simulada y real, intercambiable por variable de entorno
  (`BLOCKCHAIN_GATEWAY_MODE`), permite desarrollar y probar sin depender de
  la red Polygon en todo momento.
- **Identidad visual inmutable**: el frontend real replica exactamente el
  diseño del simulador; ningún cambio visual se introduce fuera de un
  proceso de diseño explícito.

## 3. Dominios funcionales (mapeados a los módulos del simulador)

| Dominio | Módulo del simulador | Futuro subsistema técnico |
|---|---|---|
| Sitio público / Landing | Vista "Sitio Público" | `frontend/src` (Next.js, páginas públicas) |
| Colecciones | Sección `#colecciones` | API de catálogo de joyas/esmeraldas |
| Pasaporte Digital | Vista "Pasaporte Digital" | API de piezas + certificados + blockchain |
| Certificado oficial | Pasaporte Digital Deluxe | Servicio de generación de certificados (PDF/QR) |
| SIEGEM Lab | Vista "SIEGEM Lab" | Módulo de IA (`ai/`) + API de inferencia |
| Blockchain Experience | Tabs dentro del Pasaporte | Módulo `blockchain/` (EmeraldChain) |
| Centro de Operaciones | Vista "Centro de Operaciones" | Backoffice: auth, roles, inventario, auditoría |

## 4. Stack tecnológico

| Capa | Tecnología |
|---|---|
| Frontend | HTML5, CSS3, JavaScript, TypeScript, React, Next.js |
| Backend | Python, FastAPI |
| Base de datos | PostgreSQL + SQLAlchemy (ORM) |
| Autenticación | JWT |
| IA | PyTorch, OpenCV, YOLO |
| Blockchain | Polygon, Solidity (Smart Contracts), MetaMask (wallet) |
| Storage | Supabase (datos/archivos), IPFS vía Pinata (metadatos NFT) |
| Contenedores | Docker |
| Repositorio | GitHub (GitHub Desktop compatible) |

## 5. Estructura de carpetas y su rol

```
Terrae/
├── frontend/
│   ├── simulator/     → Fuente de verdad visual (HTML original, intacto)
│   ├── public/         → Activos estáticos de la app real (etapa 3+)
│   └── src/             → Código React/Next.js real (etapa 3+)
├── backend/
│   └── app/
│       ├── domain/        → Entidades y reglas de negocio puras (futuro)
│       ├── application/    → Casos de uso / servicios (futuro)
│       ├── infrastructure/  → Repositorios, DB, blockchain gateway (futuro)
│       └── api/               → Routers FastAPI, DTOs (futuro)
├── database/
│   ├── migrations/     → Migraciones (Alembic, etapa 5)
│   └── seeds/           → Datos de referencia (piezas TR-2026-00842, etc.)
├── blockchain/
│   ├── contracts/      → Smart contracts Solidity (EmeraldChain)
│   └── scripts/         → Scripts de despliegue/verificación
├── ai/
│   ├── models/          → Modelos entrenados (EfficientNetB0, U-Net, etc.)
│   └── datasets/         → Datasets de inclusiones y calibración
└── docs/                 → Toda la documentación técnica del proyecto
```

## 6. Decisiones técnicas de la Etapa 1

| Decisión | Justificación |
|---|---|
| Monorepo único (`Terrae/`) | Simplifica la instalación con GitHub Desktop y la trazabilidad de commits entre frontend/backend/blockchain/IA en un proyecto de este tamaño. |
| El simulador se mueve a `frontend/simulator/` sin tocarlo | Cumple la regla obligatoria de no romper el simulador existente y lo mantiene como referencia viva mientras se construye la app real en `frontend/src`. |
| Separación por dominio (`backend`, `database`, `blockchain`, `ai`) en la raíz | Facilita que cada especialista (backend, blockchain, IA) trabaje de forma independiente y que cada etapa futura sea funcional por sí sola. |
| `.env.example` documentado desde la Etapa 1 | Deja explícita, desde el inicio, toda la configuración que necesitará el sistema completo, evitando sorpresas en etapas posteriores. |
| Licencia propietaria | El proyecto es un activo estratégico de EmGroup SAS orientado a adquisición/valuación, no un proyecto open source. |

## 7. Próximos pasos arquitectónicos (Etapa 2 en adelante)

- Etapa 2: configuración de entorno (Docker Compose, linters, formatters, scripts de arranque).
- Etapa 3: migración del simulador a componentes React reales, manteniendo el diseño pixel-perfect.
- Etapa 4: sistema de autenticación y roles (JWT + control de acceso por rol: administrador, joyero, auditor, cliente).
- Etapa 5: modelo de base de datos completo (usuarios, joyas, esmeraldas, certificados, blockchain, NFT, ventas, etc.).
