# Habilidades locales y edición de video

## Objetivo

Dotar a los especialistas de habilidades concretas, sin añadir agentes ni aplicaciones, y verificar un flujo técnico local de video en Codex.

## Problema y motivo

La oficina tiene 14 `AGENTS.md` con roles claros, pero ninguna habilidad local. Los editores aún no disponen de FFmpeg. Las instrucciones por sí solas no permiten transcribir, cortar ni exportar video.

## Alcance autorizado

- Instalar solo habilidades examinadas y pertinentes para `copy-organico`, `copy-ads` y los dos editores, cada una en el ámbito de su agente.
- Adaptar las instrucciones necesarias para español y evitar actualizaciones automáticas de fuentes externas.
- Preparar FFmpeg y realizar una prueba técnica con material sintético; la prueba editorial con metraje real queda pendiente hasta disponer de un archivo autorizado.
- Inicializar Git **solo localmente** para registrar unidades de trabajo; no crear remoto, publicar, instalar plugins ni construir una aplicación.
- No añadir habilidades a orquestadores ni gestores de canales. Posponer `web-design-guidelines` por su descarga de reglas mutables y Remotion por ser una alternativa, no una dependencia.

## Restricciones y aceptación

- Los entregables y las instrucciones propias de la oficina estarán en español neutro. Los archivos originales de terceros se identificarán como dependencias externas y se revisarán antes de incorporarlos.
- Las habilidades estarán bajo `<agente>/.agents/skills/<habilidad>/SKILL.md`; se comprobará el descubrimiento desde la carpeta de cada agente.
- No se ejecutarán instaladores remotos con `npx` ni comandos de actualización automática de habilidades sin nueva revisión.
- `copy-organico` no publicará ni responderá a terceros; `copy-ads` no gastará presupuesto ni invocará servicios pagos por su cuenta.
- Los editores deberán distinguir superposiciones de cortes reales, usar transcripción compatible con español y revisar el MP4 final.
- No se afirmará calidad editorial sin una prueba sobre metraje real autorizado.

## Tareas

- [x] **T1 — Incorporar habilidades de copy.** Ruta delegada; disparadores: preparación y escritura de varios archivos. `social` quedó solo en `copy-organico` y `ad-creative` solo en `copy-ads`; ambos roles tienen límites explícitos. Commit de implementación: `87a4a6a365670337cd751f282318b5178094776e`.
- [ ] **T2 — Preparar editores y habilidades de video.** Ruta delegada; disparadores: lectura amplia, adaptación de varias habilidades y archivos. Incorporar únicamente el flujo HyperFrames necesario para edición real y exportación, fijar fuentes y desactivar actualización implícita; instrucciones de uso en español y verificación estructural. Commit: pendiente.
- [ ] **T3 — Preparar FFmpeg y ejecutar prueba técnica.** Ruta delegada; disparadores: instalación y ejecución de herramientas externas. Instalar en espacio de usuario si es viable; verificar `ffmpeg`, `ffprobe`, H.264 y render corto sobre material sintético. Registrar resultados y límites. Commit: pendiente si hay archivos de proyecto; la instalación local externa se documentará sin versionar binarios.

## Verificación

- TDD estricto: habilitado por instrucciones de la sesión; no existe runner previo. Las copias y adaptaciones documentales se comprobarán mediante pruebas estructurales antes y después; si se introduce código, usar `python3 -m unittest discover -s tests -v` con RED → GREEN → REFACTOR.
- Comprobar rutas, `name` y `description` de cada `SKILL.md`, referencias locales, límites de autoridad y ausencia de actualizaciones automáticas.
- Comprobar duración, dimensiones, pista de audio y reproducción del MP4 final; la vista previa no basta.
- Estrategia de entrega: `ask-on-risk`. Previsión aproximada de cambios authored: 300–600 líneas, más archivos originales de terceros; se revisará el tamaño real por unidades de trabajo antes de cualquier PR. No se prevé PR ni remoto.

## Progreso

- Estado: T1 completada; T2 y T3 pendientes.
- Rama local: `feat/agent-skills-video`; línea base: `2f8778c`.
- Fuente T1: `coreyhaines31/marketingskills`, revisión fija `5b2c0007766c6a1cf1d53fd8fc73e979e0821022`, licencia MIT conservada en cada habilidad. Los archivos de terceros siguen en inglés; las instrucciones propias son españolas. No se incluyen los archivos de evaluación, que no son necesarios para ejecutar las habilidades.
- Verificación T1: comprobación RED previa falló por ausencia de `social/SKILL.md`; después, `quick_validate.py` aprobó ambas habilidades, la prueba estructural confirmó rutas, frontmatter, licencia, ausencia de archivos con permiso de ejecución y límites de autoridad, y `git diff --cached --check` terminó sin errores. No se ejecutó ningún script de terceros; la plantilla HTML de `ad-creative` contiene JavaScript que no se abrió ni probó. Prueba funcional de descubrimiento por Codex pendiente. Los enlaces de `ad-creative` a herramientas externas y a otra habilidad de su repositorio original no se instalaron y no deben seguirse automáticamente.
- Reversión T1: retirar únicamente las carpetas de habilidades de los dos agentes y los párrafos añadidos a sus `AGENTS.md`; no afecta a otros roles.
- Próximo paso: T2.
