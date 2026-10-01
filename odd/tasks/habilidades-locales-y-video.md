# Habilidades locales y edición de video

## Objetivo

Dotar a los especialistas de habilidades concretas, sin añadir agentes ni aplicaciones, y verificar un flujo técnico local de video en Codex.

## Problema y motivo

Al iniciar este trabajo, la oficina tenía 14 `AGENTS.md` con roles claros, pero ninguna habilidad local. Los editores aún no disponen de FFmpeg ni de un binario HyperFrames comprobado. Las instrucciones por sí solas no permiten transcribir, cortar ni exportar video.

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
- [x] **T2 — Preparar editores y habilidades de video.** Ruta delegada; disparadores: lectura amplia, adaptación de varias habilidades y archivos. Cada editor recibió `general-video`, `hyperframes-core` y `hyperframes-cli` locales, adaptadas para cortes reales y exportación sin actualización implícita. Commit de implementación: `87a927623e5b3ccd16870829de29dd2b45f6a62d`.
- [x] **T3 — Preparar FFmpeg, CLI HyperFrames y ejecutar prueba técnica.** Ruta delegada; disparadores: instalación y ejecución de herramientas externas. Se instalaron FFmpeg/FFprobe y `hyperframes@0.8.105` solo en espacio de usuario. Un montaje sintético de dos segundos se exportó con corte real y audio, incluso con la red aislada. Corrección de habilidades: `cabb0ecb03ea0fc51578727788f76faa7348ff5b`; los binarios no se versionaron.

## Verificación

- TDD estricto: habilitado por instrucciones de la sesión; no existe runner previo. Las copias y adaptaciones documentales se comprobarán mediante pruebas estructurales antes y después; si se introduce código, usar `python3 -m unittest discover -s tests -v` con RED → GREEN → REFACTOR.
- Comprobar rutas, `name` y `description` de cada `SKILL.md`, referencias locales, límites de autoridad y ausencia de actualizaciones automáticas.
- Comprobar duración, dimensiones, pista de audio y reproducción del MP4 final; la vista previa no basta.
- Estrategia de entrega: `ask-on-risk`. Previsión aproximada de cambios authored: 300–600 líneas, más archivos originales de terceros; se revisará el tamaño real por unidades de trabajo antes de cualquier PR. No se prevé PR ni remoto.

## Progreso

- Estado: T1, T2 y T3 completadas. El render técnico funciona con material sintético; la calidad editorial y la transcripción en español no están probadas.
- Rama local: `feat/agent-skills-video`; línea base: `2f8778c`.
- Fuente T1: `coreyhaines31/marketingskills`, revisión fija `5b2c0007766c6a1cf1d53fd8fc73e979e0821022`, licencia MIT conservada en cada habilidad. Los archivos de terceros siguen en inglés; las instrucciones propias son españolas. No se incluyen los archivos de evaluación, que no son necesarios para ejecutar las habilidades.
- Verificación T1: comprobación RED previa falló por ausencia de `social/SKILL.md`; después, `quick_validate.py` aprobó ambas habilidades, la prueba estructural confirmó rutas, frontmatter, licencia, ausencia de archivos con permiso de ejecución y límites de autoridad, y `git diff --cached --check` terminó sin errores. No se ejecutó ningún script de terceros; la plantilla HTML de `ad-creative` contiene JavaScript que no se abrió ni probó. Prueba funcional de descubrimiento por Codex pendiente. Los enlaces de `ad-creative` a herramientas externas y a otra habilidad de su repositorio original no se instalaron y no deben seguirse automáticamente.
- Reversión T1: retirar únicamente las carpetas de habilidades de los dos agentes y los párrafos añadidos a sus `AGENTS.md`; no afecta a otros roles.
- Fuente T2: `heygen-com/hyperframes`, revisión fija `8593b01a6d0df887aa111a1d0871c42c5343fab1`, licencia Apache-2.0 conservada en cada habilidad. Se conservaron solo referencias técnicas para cortes y composición; se retiraron scripts, subagentes y referencias de servicios remotos. Los `SKILL.md` adaptados y los límites de cada editor están en español. `talking-head-recut` no se instaló porque reproduce el metraje completo con superposiciones y su ejemplo de transcripción usa `small.en`.
- Verificación T2: comprobación RED previa falló por ausencia de `general-video/SKILL.md`; después, `quick_validate.py` aprobó las seis habilidades, la prueba estructural confirmó rutas, frontmatter, licencias, enlaces locales y ausencia de archivos ejecutables; las referencias conservadas coincidieron con la revisión fijada tras normalizar el reemplazo de `npx` por el ejecutable local. `git diff --cached --check` terminó sin errores. No se ejecutó el CLI ni se renderizó video: faltan binario y FFmpeg; el rendimiento y la calidad editorial siguen sin verificar.
- Reversión T2: retirar únicamente las tres carpetas de habilidades de cada editor y los párrafos añadidos a sus `AGENTS.md`; no afecta a los agentes de copy.
- Fuente T3 (FFmpeg): el sitio oficial de FFmpeg enlaza las compilaciones Linux de BtbN. Se obtuvo el artefacto público `ffmpeg-n9.0-latest-linux64-gpl-9.0.tar.xz` del release BtbN `400993884`, asset `603324015`, publicado el 2026-10-01. Su SHA-256 comprobado es `72509b592457c9dca4aeaa59cee3b8ddca11ba2d71d70800bb2ad0f4cfe129a2`; se examinó el archivo antes de extraer únicamente `ffmpeg`, `ffprobe` y `LICENSE.txt` (GPLv3). Instalación: `~/.local/opt/ffmpeg/btbn-n9.0-asset603324015/`; enlaces añadidos, antes ausentes: `~/.local/bin/ffmpeg` y `~/.local/bin/ffprobe`. Ambos informan `n9.0.2-22-g46d8f462ee-20261001` y el codificador `libx264` está disponible. Fuentes: <https://www.ffmpeg.org/download.html> y <https://github.com/BtbN/FFmpeg-Builds/releases>.
- Fuente T3 (HyperFrames): el paquete publicado es **`hyperframes@0.8.105`**, no `@hyperframes/cli` (este último devolvió 404). Se instaló con `npm ci --ignore-scripts --no-audit --no-fund` en `~/.local/opt/hyperframes/0.8.105/`, junto a `gsap@3.14.2`; sin npm global ni `npx`. Integridades del registro npm: HyperFrames `sha512-Htr0cE6HTEPXNsPJ4KOi4gokB/HE1njjp1cIdWX7oGgQo3zsVB0YimGpYHRRCeQNb6lNiJQPlGc1WVnGfweHBA==`; GSAP `sha512-P8/mMxVLU7o4+55+1TCnQrPmgjPKnwkzkXOK1asnR9Jg2lna4tEY5qBJjMmAaOBDDZWtlRjBXjLa0w53G/uBLA==`. El paquete declara `gitHead=bc57e282fdde4afdccec1d1a2bacd94a9c3c5383`; la comparación con la revisión de habilidades T2 no mostró cambios en `packages/cli` ni `skills/`. Enlace añadido, antes ausente: `~/.local/bin/hyperframes`. Versión comprobada: `0.8.105`. Fuente: <https://github.com/heygen-com/hyperframes> y <https://registry.npmjs.org/hyperframes/0.8.105>.
- Corrección observada durante T3: los dos `hyperframes-cli/SKILL.md` y tres referencias `hyperframes-core` de cada editor usaban el nombre de paquete inexistente o una ruta `./node_modules/.bin/hyperframes` que no corresponde a esta instalación. Se actualizaron a `hyperframes` local fijado; `quick_validate.py` pasó para las cuatro habilidades implicadas, la prueba estructural de ocho archivos pasó y `git diff --check` no detectó errores. La prueba RED previa falló al exigir el paquete publicado y GREEN pasó tras corregirlo. Se usan `HYPERFRAMES_NO_TELEMETRY=1` y `HYPERFRAMES_SKIP_SKILLS=1` para evitar telemetría y consulta automática de habilidades.
- Prueba T3: proyecto descartable fuera del repositorio en `~/.local/share/oficina/prueba-video-sintetico-20261001/`, con clips sintéticos rojo, verde y azul, tonos AAC y GSAP local. La composición toma el primer segundo rojo y el tercer segundo azul: omite el tramo verde mediante cortes reales, no superposiciones. `hyperframes lint --json` y `hyperframes check --json --samples 3` devolvieron `ok: true` sin avisos. Tras una primera descarga pública de Chrome Headless Shell a `~/.cache/hyperframes/chrome/chrome-headless-shell/linux-152.0.7977.30/`, el render final se ejecutó con `bwrap --unshare-net`, sin acceso de red. `output-final.mp4` tiene SHA-256 `09e4a735f7aa857d643be54fcdb47f9a374e0274906638868bd43bfd6d9830c0`; `ffprobe` confirmó 2,000 s, 320 × 180, H.264 y AAC a 48 kHz. Fotogramas a 0,5 y 1,5 s muestran rojo y azul; inspección de audio detectó señal sin silencios largos. El segundo render usa fuente con fotogramas clave cada 24 cuadros y no repitió el aviso inicial de GOP disperso.
- Límites T3: `hyperframes doctor --json` terminó con código cero, pero `ok: false` por complementos opcionales de transcripción, voz y música ausentes; Node, FFmpeg, FFprobe y navegador están disponibles. No se probó Whisper ni una transcripción en español; `transcribe --help` muestra un predeterminado `small.en`, por lo que deberá elegirse un modelo multilingüe e idioma `es` para esa tarea. Tampoco se evaluó metraje real, subtítulos, publicación ni calidad editorial. La primera renderización puede descargar Chrome; los siguientes renders pueden hacerse sin red con assets locales, como se verificó aquí.
- Reversión T3: eliminar `~/.local/bin/{ffmpeg,ffprobe,hyperframes}` **solo si** siguen apuntando a estas instalaciones y luego borrar `~/.local/opt/ffmpeg/btbn-n9.0-asset603324015/` y `~/.local/opt/hyperframes/0.8.105/`. La prueba sintética se puede borrar de `~/.local/share/oficina/prueba-video-sintetico-20261001/`; la caché específica del Chrome descargado está bajo `~/.cache/hyperframes/chrome/chrome-headless-shell/linux-152.0.7977.30/`. No se modificaron instalaciones globales.
- Próximo paso opcional: prueba editorial con metraje real autorizado y escucha humana del montaje; validar transcripción española solo si un flujo la necesita.
