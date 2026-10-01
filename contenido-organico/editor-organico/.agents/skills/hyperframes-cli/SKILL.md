---
name: hyperframes-cli
description: Úsala para inspeccionar, comprobar, previsualizar y exportar localmente una composición HyperFrames, o para diagnosticar fallos del render y verificar el MP4 resultante.
---

# Operación local de HyperFrames

Fuente: `heygen-com/hyperframes` en la revisión `8593b01a6d0df887aa111a1d0871c42c5343fab1` (Apache-2.0). Esta edición local elimina rutas automáticas de instalación, actualización y servicios remotos.

Adaptación limitada de `heygen-com/hyperframes` para esta oficina. Requiere Node.js 22 o superior, FFmpeg/FFprobe y una versión revisada de `@hyperframes/cli` instalada y fijada en el proyecto. Antes de ejecutarla, comprueba la presencia de `./node_modules/.bin/hyperframes`; si falta, informa el bloqueo. **No uses `npx`**, que podría descargar y ejecutar una versión no revisada. Ejecuta desde la raíz del proyecto de video, no desde la raíz de la oficina.

Desactiva la telemetría en cada proceso con `HYPERFRAMES_NO_TELEMETRY=1`. No utilices `feedback`, `publish`, `cloud`, `cloudrun`, `lambda`, `auth`, `upgrade`, `skills update` ni servicios externos. No cambies la versión fijada del paquete ni instales dependencias sin autorización.

## Ciclo local

1. `HYPERFRAMES_NO_TELEMETRY=1 ./node_modules/.bin/hyperframes doctor`: comprueba requisitos; si solicita instalación o descarga, detente.
2. Antes de editar un proyecto existente, `HYPERFRAMES_NO_TELEMETRY=1 ./node_modules/.bin/hyperframes timeline --json`: identifica clips y rangos reales.
3. Después del montaje, ejecuta `HYPERFRAMES_NO_TELEMETRY=1 ./node_modules/.bin/hyperframes lint` y luego `HYPERFRAMES_NO_TELEMETRY=1 ./node_modules/.bin/hyperframes check`. Corrige los errores antes de exportar.
4. Examina una vista previa local y fotogramas representativos. Para una pieza destinada a entrega, presenta la vista previa al usuario u orquestador y espera la aprobación del montaje antes del render final. Una prueba técnica sintética ya autorizada puede renderizarse sin aprobación editorial.
5. Exporta con el ejecutable local, por ejemplo `HYPERFRAMES_NO_TELEMETRY=1 ./node_modules/.bin/hyperframes render --quality looks --output salida.mp4`.
6. Comprueba con `ffprobe` duración, dimensiones, códec y pista de audio; reproduce el MP4, escucha al menos el inicio, cortes y final, y revisa fotogramas de cada tramo. Reporta lo no verificado.

La transcripción, si se necesita, debe funcionar con español: inspecciona `transcribe --help`, elige un modelo multilingüe y especifica idioma `es` solo si esa versión acepta la opción. Nunca uses un modelo `.en` ni presupongas exactitud sin escuchar muestras. No envíes audio a servicios remotos sin autorización.
