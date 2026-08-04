# Manual de Instalación — Etapa 1

## Alcance de esta etapa

En la Etapa 1 el repositorio contiene únicamente **estructura, documentación
y el simulador visual**. No hay backend, base de datos, IA ni blockchain
ejecutándose todavía — eso llegará en etapas posteriores, cada una con su
propio manual de instalación actualizado.

## Requisitos previos

- [GitHub Desktop](https://desktop.github.com/) (recomendado) o Git CLI.
- Un navegador web moderno (Chrome, Edge, Safari, Firefox) para ver el
  simulador.
- Cuenta de GitHub con acceso al repositorio `Terrae`.

## Instalación local con GitHub Desktop

1. Abrir **GitHub Desktop**.
2. `File → Clone Repository...`
3. Seleccionar el repositorio `Terrae` (o pegar la URL si aún no aparece en
   la lista).
4. Elegir una carpeta local (por ejemplo `Documentos/Terrae`).
5. Clic en **Clone**.
6. Verificar que la carpeta local contiene la estructura descrita en
   `README.md` y `docs/ARQUITECTURA.md`.

## Instalación local con Git (alternativa)

```bash
git clone https://github.com/<tu-usuario>/Terrae.git
cd Terrae
git status
```

## Ver el simulador

El simulador es un archivo HTML autocontenido (HTML + CSS + JS en un único
archivo), sin dependencias ni build necesario:

```bash
cd Terrae/frontend/simulator
# Opción 1: abrir directamente
open index.html          # macOS
start index.html         # Windows
xdg-open index.html      # Linux

# Opción 2 (recomendada): servirlo con un servidor local simple
python3 -m http.server 5500
# luego abrir http://localhost:5500 en el navegador
```

> Se recomienda la Opción 2 para evitar restricciones del navegador con
> rutas `file://` al avanzar en etapas donde el simulador empiece a
> consumir la API real.

## Configuración de variables de entorno

1. Copiar el archivo de referencia:
   ```bash
   cp .env.example .env
   ```
2. En esta etapa **no es necesario completar ningún valor real**; el archivo
   `.env` solo documenta las variables que usarán las próximas etapas
   (backend, base de datos, blockchain, IA, storage).
3. El archivo `.env` está excluido de Git mediante `.gitignore` — nunca debe
   subirse al repositorio.

## Validación de la instalación (Etapa 1)

Ejecutar el checklist de `docs/ARQUITECTURA.md` §6 y confirmar:

- [ ] El repositorio clona correctamente con GitHub Desktop.
- [ ] La estructura de carpetas coincide con la documentada en `README.md`.
- [ ] `frontend/simulator/index.html` abre en el navegador y se ve
      idéntico al simulador original (sin errores en consola).
- [ ] Los 4 logotipos de marca están presentes en
      `frontend/simulator/assets/brand/`.
- [ ] `.env.example` existe y `.env` (si se creó) no aparece en
      `git status` gracias al `.gitignore`.

## Próxima etapa

La **Etapa 2 (Configuración del entorno y herramientas)** añadirá:
Docker Compose, configuración de linters/formatters, scripts de arranque
unificados (`scripts/`), y la base del proyecto Next.js en `frontend/src`.
