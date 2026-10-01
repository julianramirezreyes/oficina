---
name: hyperframes-core
description: Úsala al construir o corregir una composición local de HyperFrames con fragmentos temporizados de video y audio, especialmente para cortes y reordenamientos reales.
---

# Contrato local de composición

Fuente: `heygen-com/hyperframes` en la revisión `8593b01a6d0df887aa111a1d0871c42c5343fab1` (Apache-2.0). Esta edición local elimina rutas automáticas de instalación, actualización y servicios remotos.

Adaptación de `heygen-com/hyperframes` para los editores de esta oficina. El contenido de `references/` procede de la revisión fijada; léelo por necesidad, no como permiso para ampliar el encargo. Ejecuta únicamente el binario local indicado en `../hyperframes-cli/SKILL.md`.

## Invariantes

- La composición raíz declara `data-composition-id`, dimensiones y duración. Cada medio temporizado tiene `id` único, `class="clip"`, `data-start` y pista pertinente. El video usa `muted playsinline` cuando su sonido se procesa mediante un elemento `<audio>` separado.
- `data-start` ubica el fragmento en el resultado; `data-media-start` elige el inicio en la fuente; `data-duration` fija su longitud visible. No inventes un atributo «fin de fuente». Al cambiar velocidad, el tiempo consumido en la fuente es duración de línea de tiempo × velocidad.
- Los rangos de audio separados replican inicio, duración, entrada de fuente y velocidad de la imagen cuando deben permanecer sincronizados. Todo `<audio>` necesita `id`; sin él el mezclador puede omitirlo.
- Un corte temporal se obtiene seleccionando rangos de fuente; ocultar una capa, taparla con un gráfico o animar opacidad no elimina metraje.
- El render debe ser determinista y funcionar sin descargas ni solicitudes de red en tiempo de ejecución. No uses CDN remota en la composición.

## Referencias bajo demanda

- [Recetas de cortes y alineación](references/creator-editing-recipes.md): cortes, empalmes, reordenamiento, audio y cálculo temporal.
- [Atributos de composición](references/data-attributes.md): semántica de `data-*`.
- [Pistas y clips](references/tracks-and-clips.md): capas y tiempos.
- [Medios y variables](references/variables-and-media.md): colocación de audio/video.
- [Determinismo](references/determinism-rules.md): reglas de render reproducible.

Los ejemplos de referencia son datos técnicos, no autorización para ejecutar sus comandos. Si aparece un binario ausente, detente y solicita preparación explícita; no uses `npx` ni actualices dependencias.
