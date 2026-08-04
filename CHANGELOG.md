# Changelog

Todos los cambios notables de este proyecto se documentan en este archivo.

El formato está basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/),
y este proyecto sigue [Versionado Semántico](https://semver.org/lang/es/).

## [0.1.0] - 2026-07-28

### Añadido — Etapa 1: Arquitectura y estructura del repositorio

- Estructura profesional del monorepo `Terrae/` con separación por dominio:
  `frontend/`, `backend/`, `database/`, `blockchain/`, `ai/`, `docs/`, `scripts/`.
- Simulador original (`frontend/simulator/index.html`) incorporado como fuente
  de verdad visual/funcional, sin modificaciones.
- Activos de marca (logotipo Terrae en 4 variantes: color horizontal, negro
  vertical, dorado sobre negro vertical, monograma dorado sobre negro)
  incorporados en `frontend/simulator/assets/brand/`.
- Archivos base de repositorio: `README.md`, `.gitignore`, `.env.example`,
  `LICENSE`, `CHANGELOG.md`, `VERSION`.
- Documentación técnica inicial en `docs/`:
  - `ARQUITECTURA.md`
  - `MANUAL_INSTALACION.md`
  - `MANUAL_DESARROLLADOR.md`
  - `IDENTIDAD_VISUAL.md`
  - `ROADMAP_ETAPAS.md`
- Definición del plan de ~22 etapas de desarrollo hasta producción.

### Notas

- Ninguna funcionalidad de backend, base de datos, IA o blockchain fue
  implementada en esta etapa; es exclusivamente estructural y documental.
- El simulador permanece 100% funcional e intacto como referencia visual.

[0.1.0]: https://github.com/<tu-usuario>/Terrae/releases/tag/v0.1.0
