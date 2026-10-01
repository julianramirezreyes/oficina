---
name: general-video
description: Úsala cuando un video existente necesite cortes reales, recortes de entrada o salida, empalmes, reordenamiento de fragmentos o montaje de varias tomas con HyperFrames.
---

# Montaje local de video

Fuente: `heygen-com/hyperframes` en la revisión `8593b01a6d0df887aa111a1d0871c42c5343fab1` (Apache-2.0). Esta edición local elimina rutas automáticas de instalación, actualización y servicios remotos.

Adaptación local de `heygen-com/hyperframes` en la revisión fijada para esta oficina. Consulta `../hyperframes-core/SKILL.md` para el contrato de composición y `../hyperframes-cli/SKILL.md` para las operaciones locales. Las instrucciones del `AGENTS.md` del editor prevalecen.

## Preparación

1. Confirma guion, metraje y audio autorizados, formato, duración y destino. No añadas material externo ni cambies afirmaciones comerciales por iniciativa propia.
2. Comprueba que existen FFmpeg, FFprobe y el ejecutable local de HyperFrames fijado en el proyecto. Si falta alguno, informa el bloqueo; esta habilidad no autoriza instalarlo ni descargar una versión nueva.
3. Inspecciona duración, dimensiones, frecuencia de cuadros y pistas de audio de cada fuente. Si el corte depende de la voz, usa una transcripción multilingüe compatible con español; nunca `small.en`. Corrige nombres y marcas de tiempo importantes escuchando el original.
4. Define una lista de segmentos conservados: archivo, entrada y salida de fuente, posición en la línea de tiempo, audio correspondiente y motivo editorial. Señala claramente el material omitido.

## Corte y montaje

- Para un corte auténtico, asigna a cada fragmento `data-media-start` (entrada en la fuente), `data-duration` (longitud en la línea de tiempo) y `data-start` (posición final). Calcula `salida de fuente = entrada + duración × velocidad`. No uses una capa gráfica para simular un recorte.
- Consulta solo las secciones necesarias de `../hyperframes-core/references/creator-editing-recipes.md`: **Hard cut**, **Trim in/out**, **Split / splice**, **Reorder** y **Audio alignment**. Da identificadores únicos a los clips y separa video silenciado de audio cuando ambos necesiten los mismos cortes.
- Ajusta la duración de la composición al último fragmento. Comprueba que no haya huecos negros accidentales, audio continuo cuando no corresponde ni palabras cortadas.
- Los rótulos, imágenes y subtítulos son capas adicionales; no sustituyen los cortes. Si se solicitan, intégralos después de estabilizar el montaje principal.

## Validación y entrega

Sigue el ciclo local de `hyperframes-cli`: línea de tiempo, comprobación, vista previa, exportación autorizada y examen del MP4. Verifica el archivo exportado, no solo el HTML o la vista previa. Informa duración, formato, audio, fragmentos usados, fuentes y problemas pendientes. Una prueba sintética demuestra viabilidad técnica, no calidad editorial.

No publiques, actives campañas, uses renderizado en la nube, envíes telemetría/comentarios ni invoques APIs pagas. No actualices habilidades ni el paquete automáticamente.
