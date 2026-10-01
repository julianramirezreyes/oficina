---
name: hyperframes-cli
description: Úsala para inspeccionar, comprobar, previsualizar y exportar localmente una composición HyperFrames, o para diagnosticar fallos del render y verificar el MP4 resultante.
---

# Operación local de HyperFrames

Fuente: `heygen-com/hyperframes` en la revisión `8593b01a6d0df887aa111a1d0871c42c5343fab1` (Apache-2.0). Esta edición local elimina rutas automáticas de instalación, actualización y servicios remotos.

Adaptación limitada de `heygen-com/hyperframes` para esta oficina. Requiere Node.js 22 o superior, FFmpeg/FFprobe y una versión revisada de `hyperframes@0.8.105` instalada en espacio de usuario. Antes de ejecutarla, comprueba que `command -v hyperframes` apunta a una instalación local fijada y que `hyperframes --version` devuelve `0.8.105`; si falta o difiere, informa el bloqueo. **No uses `npx`**, que podría descargar y ejecutar una versión no revisada. Ejecuta desde la raíz del proyecto de video, no desde la raíz de la oficina.

Desactiva la telemetría y la consulta automática de habilidades en cada proceso con `HYPERFRAMES_NO_TELEMETRY=1 HYPERFRAMES_SKIP_SKILLS=1`. El comando `init` consulta GitHub si falta la segunda variable. No utilices `feedback`, `publish`, `cloud`, `cloudrun`, `lambda`, `auth`, `upgrade`, `skills update` ni servicios externos. No cambies la versión fijada del paquete ni instales dependencias sin autorización.

## Ciclo local

1. `HYPERFRAMES_NO_TELEMETRY=1 HYPERFRAMES_SKIP_SKILLS=1 hyperframes doctor`: comprueba requisitos; si solicita instalación o descarga, detente. Su campo `ok` puede ser falso por extras opcionales como Whisper o síntesis de voz: identifica cuáles faltan antes de concluir que el render local está bloqueado.
2. Antes de editar un proyecto existente, `HYPERFRAMES_NO_TELEMETRY=1 HYPERFRAMES_SKIP_SKILLS=1 hyperframes timeline --json`: identifica clips y rangos reales.
3. Después del montaje, ejecuta `HYPERFRAMES_NO_TELEMETRY=1 HYPERFRAMES_SKIP_SKILLS=1 hyperframes lint` y luego `HYPERFRAMES_NO_TELEMETRY=1 HYPERFRAMES_SKIP_SKILLS=1 hyperframes check`. Corrige los errores antes de exportar.
4. El primer render puede descargar Chrome Headless Shell si aún no existe en caché; confirma que esa descarga está autorizada y registra la ruta. Examina una vista previa local y fotogramas representativos. Para una pieza destinada a entrega, presenta la vista previa al usuario u orquestador y espera la aprobación del montaje antes del render final. Una prueba técnica sintética ya autorizada puede renderizarse sin aprobación editorial.
5. Exporta con el ejecutable local, por ejemplo `HYPERFRAMES_NO_TELEMETRY=1 HYPERFRAMES_SKIP_SKILLS=1 hyperframes render --quality looks --output salida.mp4`.
6. Comprueba con `ffprobe` duración, dimensiones, códec y pista de audio; reproduce el MP4, escucha al menos el inicio, cortes y final, y revisa fotogramas de cada tramo. Reporta lo no verificado.

Al crear una composición sin red, usa recursos JavaScript locales; no cargues GSAP desde CDN.

## Transcripción local en español

1. Comprueba la disponibilidad de Parakeet local. Ejecuta `HYPERFRAMES_NO_TELEMETRY=1 HYPERFRAMES_SKIP_SKILLS=1 hyperframes transcribe audio.wav --engine parakeet --language es --json`.
2. Exige `engine: parakeet` en el resultado. El motor explícito evita volver silenciosamente al predeterminado de Whisper `small.en`. Si Parakeet falta o falla, informa el bloqueo; no instales modelos ni cambies de motor por tu cuenta. `doctor --json` puede seguir mostrando Whisper como complemento ausente aunque Parakeet funcione.
3. Revisa las palabras y marcas de tiempo escuchando el original. Corrige nombres propios, cifras y términos del negocio antes de crear subtítulos. No envíes audio a servicios remotos sin autorización.
