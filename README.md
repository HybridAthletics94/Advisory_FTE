# Astara Advisory FTE Planner · MVP GitHub Pages

HTML estático para planificar FTEs del equipo de Advisory por persona, proyecto y semana, con resumen semanal/mensual y sincronización simple mediante un fichero JSON versionado en GitHub.

## Estructura del proyecto

```txt
advisory-fte-planner-mvp/
├─ index.html
├─ data/
│  └─ planner.json
├─ README.md
├─ .nojekyll
└─ .gitignore
```

## Qué incluye

- Matriz editable de FTEs por proyecto, persona y semana.
- Cambio de fecha de inicio por proyecto sin perder la planificación relativa.
- Resumen por semana o por mes.
- Semáforo de uso de capacidad por equipo y persona.
- Gestión de proyectos y personas.
- Guardado local automático en el navegador.
- Export/import JSON.
- Sincronización MVP con GitHub: **Actualizar desde GitHub** y **Publicar cambios**.

## Publicación rápida en GitHub Pages

1. Crea un repositorio en GitHub, por ejemplo `advisory-fte-planner`.
2. Sube todo el contenido de esta carpeta a la raíz del repo.
3. En GitHub, entra en **Settings → Pages**.
4. En **Build and deployment**, selecciona **Deploy from a branch**.
5. Elige branch `main` y carpeta `/ (root)`.
6. Guarda y abre la URL de GitHub Pages cuando esté publicada.


## Barrera básica de acceso

Este MVP incluye una landing inicial con password manual. La clave no se guarda en texto plano en el HTML: se compara mediante un hash SHA-256 en cliente.

Importante: esto es una barrera básica para evitar accesos casuales, no una autenticación real. Si GitHub Pages o el repositorio son públicos, una persona con conocimientos técnicos podría inspeccionar el código o acceder directamente al JSON publicado.

Para cambiar la clave:

1. Calcula el hash SHA-256 de la nueva clave.
2. Abre `index.html`.
3. Sustituye el valor de `ACCESS_PASSWORD_HASH`.
4. Sube el cambio a GitHub.

El password de acceso no debe ser el token de GitHub. El token solo se usa para publicar cambios en `data/planner.json`.

## Configurar la sincronización de datos

La pestaña **Datos y publicación** ya viene configurada para:

- **Owner / organización:** `hybridathletics94`
- **Repositorio:** `Advisory_FTE`
- **Branch:** `main`
- **Ruta JSON:** `data/planner.json`

Solo tienes que pegar el **Token GitHub para publicar**.

Después:

- Pulsa **Guardar token**.
- Pulsa **Actualizar desde GitHub** para traer la versión publicada de `data/planner.json`.
- Edita la planificación.
- Pulsa **Publicar cambios** para guardar la planificación en GitHub con un commit.

## Token recomendado para el MVP

Crea un **fine-grained personal access token** limitado solo a este repositorio y con permiso:

- Repository permissions → **Contents: Read and write**

No pegues el token en el código ni lo subas al repositorio. La herramienta lo guarda solo en `sessionStorage`, es decir, en la sesión del navegador.

## Flujo recomendado de trabajo

1. Abrir la web.
2. Ir a **Datos y publicación**.
3. Pulsar **Actualizar desde GitHub** antes de editar.
4. Hacer cambios.
5. Revisar el resumen.
6. Pulsar **Publicar cambios**.

Si dos personas editan a la vez, puede aparecer un conflicto. En ese caso: actualizar desde GitHub, revisar los cambios y volver a publicar.

## Nota de seguridad

Este MVP usa GitHub Pages y un JSON publicado en el repo. Si el site o el repo son públicos, los datos también pueden ser visibles públicamente. Para datos reales de equipo/proyecto, usa repo privado y visibilidad privada de Pages si está disponible en la organización, o evoluciona el MVP a una solución con autenticación.


## Cambios UX de esta versión

- La matriz de FTEs usa campos de texto decimal, no `input type=number`, para evitar que las flechas del teclado suban/bajen el valor.
- En la matriz de proyecto puedes moverte con `←`, `→`, `↑`, `↓` y `Enter` entre celdas.
- Al editar FTEs no se vuelve a renderizar toda la tab de proyecto, así que el scroll horizontal se mantiene.
- `data/planner.json` incluido en este paquete corresponde al estado publicado en GitHub en el momento de generar esta versión.
