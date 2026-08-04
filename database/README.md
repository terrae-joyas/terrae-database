# database/

Modelo de datos PostgreSQL del ecosistema Terrae — diseño completo
implementado en la Etapa 5 (24 tablas, ver
`docs/ETAPA_5_BASE_DE_DATOS.md`).

## Nota de implementación: ¿dónde están las migraciones y los seeds?

Esta carpeta se dejó como placeholder desde la Etapa 1, pero las
migraciones y la siembra de datos terminaron implementándose junto al
código de la aplicación, no aquí, por una razón concreta:

- **Migraciones (Alembic)** → `backend/alembic/`
  Alembic necesita importar `app.config.get_settings()` y
  `app.infrastructure.db.base.Base` (con todos los modelos) para
  funcionar. Ponerlo dentro de `backend/` evita imports relativos frágiles
  entre carpetas hermanas del repositorio y mantiene una sola fuente de
  verdad de configuración (el mismo `.env` que usa el backend en runtime).
- **Datos de referencia (seed)** → `backend/app/scripts/seed_db.py`
  Por el mismo motivo: la siembra reutiliza directamente los modelos
  SQLAlchemy y el `AuthService`/`UsuarioRepository` ya existentes en
  `backend/app/`, en vez de duplicar esa lógica en un script aislado.

`database/` sigue siendo el lugar de la documentación y diseño del
modelo de datos en sí (ERD, decisiones de normalización, catálogo de
tablas), que es lo que vive en `docs/ETAPA_5_BASE_DE_DATOS.md`.

## Comandos relacionados

```bash
make db-migrate      # aplica migraciones pendientes (también automático al iniciar el backend)
make db-downgrade    # revierte la última migración
make db-revision MSG="descripcion"   # genera una nueva migración autogenerada
make db-seed         # siembra usuarios demo + sucursal + esmeraldas/joyas de referencia
```

