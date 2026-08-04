# TERRAE — Ecosistema Digital

> **Lo que la tierra esconde, Terrae lo revela.**

Plataforma tecnológica para trazabilidad, certificación científica y pasaporte digital de esmeraldas y alta joyería colombiana, respaldada por inteligencia artificial (SIEGEM Lab) y blockchain (EmeraldChain).

Este repositorio es la **base técnica real** del Ecosistema Digital Terrae, construida progresivamente a partir del simulador visual/funcional ya existente (`frontend/simulator/index.html`), que define la identidad de marca, la navegación y la experiencia de usuario de referencia.

---

## 📌 Estado del proyecto

| Etapa | Nombre | Estado |
|---|---|---|
| 1 | Arquitectura y estructura del repositorio | ✅ Completada |
| 2 | Configuración del entorno y herramientas | ⏳ Pendiente |
| 3 | Migración del simulador a componentes reales | ⏳ Pendiente |
| 4 | Autenticación y roles | ⏳ Pendiente |
| 5 | Base de datos inicial | ⏳ Pendiente |
| ... | Ver `docs/ROADMAP_ETAPAS.md` | |

Versión actual: **v0.1.0** (ver `CHANGELOG.md` y `VERSION`).

---

## 🧱 Estructura del repositorio

```
Terrae/
├── frontend/            # Cliente web (simulador + futura app React/Next.js)
│   ├── simulator/        # Simulador HTML original — NO SE MODIFICA, es la fuente visual de verdad
│   ├── public/            # Activos públicos de la futura app
│   └── src/               # Código fuente de la futura app React/Next.js (etapa 3+)
├── backend/              # API REST en FastAPI (Python)
│   └── app/
├── database/             # Modelo de datos, migraciones y seeds (PostgreSQL)
│   ├── migrations/
│   └── seeds/
├── blockchain/            # Smart contracts EmeraldChain (Solidity / Polygon)
│   ├── contracts/
│   └── scripts/
├── ai/                    # Módulo SIEGEM Lab — IA gemológica (PyTorch/OpenCV/YOLO)
│   ├── models/
│   └── datasets/
├── docs/                  # Documentación técnica, manuales y arquitectura
├── scripts/                # Scripts de automatización, setup, utilidades
├── .github/workflows/       # CI/CD (a definir en etapas posteriores)
├── .gitignore
├── .env.example
├── LICENSE
├── CHANGELOG.md
└── VERSION
```

## 🎨 Identidad visual (fuente de verdad)

La identidad visual completa está definida y congelada en `frontend/simulator/index.html` y documentada en `docs/IDENTIDAD_VISUAL.md`. **Ninguna etapa futura debe alterar esta identidad**; solo debe convertirse en componentes reales.

## 🚀 Instalación rápida

Ver instrucciones completas en `docs/MANUAL_INSTALACION.md`. Resumen:

```bash
# 1. Clonar el repositorio (o abrir con GitHub Desktop)
git clone https://github.com/<tu-usuario>/Terrae.git
cd Terrae

# 2. Ver el simulador (no requiere instalación, es HTML puro)
open frontend/simulator/index.html   # macOS
# o simplemente arrastrar el archivo a un navegador
```

Los módulos de backend, base de datos, IA y blockchain se activarán en las etapas 4 en adelante, cada uno con su propio manual de instalación.

## 🗺️ Roadmap completo

Ver `docs/ROADMAP_ETAPAS.md` para el plan detallado de las ~20-25 etapas de desarrollo.

## 👥 Equipo técnico de referencia

Este proyecto se desarrolla siguiendo el **Prompt Maestro Terrae**, que define un enfoque multidisciplinario (CTO, arquitectura de software, backend, frontend, IA, blockchain, DevOps, seguridad, QA) trabajando etapa por etapa, con entrega documentada y validación en cada fase.

## 📄 Licencia

Ver `LICENSE`. Software propietario — Terrae / EmGroup SAS. Todos los derechos reservados.
