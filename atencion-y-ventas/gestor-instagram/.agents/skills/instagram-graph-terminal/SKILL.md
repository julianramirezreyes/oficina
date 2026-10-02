---
name: instagram-graph-terminal
description: "Úsala para comentarios, respuestas privadas a palabras clave, mensajes, publicación orgánica o insights de Instagram mediante la API en terminal."
---

# API de Instagram Login desde terminal

## Principio

Usa la API oficial Instagram Login en `graph.instagram.com` conforme a `AGENTS.md` del agente y de la oficina. Esta skill **no concede permisos** ni amplía el alcance autorizado.

## Preparación segura

1. Lee `AGENTS.md` del agente. Sigue exactamente su validación de identidad y carga de credenciales; no compares numéricamente `INSTAGRAM_USER_ID` con el ID devuelto por API.
2. Antes de una escritura, valida con el mismo token ambas respuestas de identidad exigidas allí. Si falta un dato, falla una consulta o no coinciden `username`/`id`, detente y escala.
3. Consulta la [colección oficial de Meta para Instagram Login](https://www.postman.com/meta/instagram/folder/6raa77c/instagram-api-with-instagram-login) para verificar versión, permisos y endpoint. Usa `graph.instagram.com`; no traslades rutas de Facebook Login ni inventes endpoints.
4. Mantén el token solo en el `.env` local indicado por `AGENTS.md`. Pásalo a `curl` mediante stdin, como en el ejemplo del agente. Nunca lo pongas en URL, argumentos, historial, archivo temporal o salida; evita `set -x`, `curl -v` y registros de cabeceras. No abras ni imprimas el contenido de `.env`; cárgalo únicamente según `AGENTS.md`.

## Lecturas antes de actuar

- **Comentarios:** pagina todos los resultados y abre cada comentario con sus respuestas/hilo completo. Si una página o hilo no se puede leer, no respondas ese hilo. Comprueba autor, contexto y respuestas existentes desde la cuenta autorizada; responde una sola vez solo si no hay respuesta. No infieras ausencia de respuesta desde la primera página.
- **Mensajes directos:** procesa conversaciones iniciadas por un mensaje entrante o una respuesta privada documentada a un comentario que solicita el recurso anunciado. Lee el contexto disponible; no inicies DMs sin esa interacción ni envíes mensajes masivos.
- **Publicación:** publica solo la pieza orgánica final recibida de contenido orgánico; no alteres oferta, condiciones ni afirmaciones. Sigue el flujo documentado y comprueba el estado final antes de reportar éxito.
- **Insights:** limita la operación a lecturas documentadas de métricas. No cambies configuración, permisos ni estado de la cuenta.

## Palabra clave → respuesta privada → recurso

Para preparación de varias publicaciones, frases clave, recursos o intervalos, sigue el [procedimiento de campañas y estado](references/campaign-workflow.md) y adapta las [plantillas de campaña](assets/campaign.template.json) y [estado](assets/state.template.json). Son configuración y registro atendidos por el agente, no un runtime de cola; no actives una campaña por haber completado una plantilla.

Al configurar una campaña, pregunta **una cosa por vez** y no repitas datos ya dados: cuenta autorizada, publicación/reel concreto, palabra clave, recurso y URL, y si el usuario prefiere texto simple o flujo con botones. Para botones, solicita el texto inicial y, para cada botón, etiqueta, tipo de acción y destino o respuesta posterior. Distingue botón que abre URL de botón de selección que exige recibir un evento y enviar un segundo mensaje. Comprueba enlaces y hechos de la oferta; muestra una vista previa del comentario elegible, primer DM, opciones y seguimiento antes de cualquier envío.

Una respuesta privada al comentario no equivale a un DM iniciado libremente. Verifica en la documentación vigente de [Private Replies](https://www.postman.com/meta/instagram/http-request/23987686-e1e3a938-1d1d-48ed-b739-1188c75759e2) y [Templates](https://www.postman.com/meta/instagram/folder/rl2amj3/templates) permisos, ventana temporal, límite por comentario y formato admitido por **Instagram Login**. La referencia externa usa Facebook Login y token de Página: no copies sus rutas ni pongas tokens en URL. La documentación consultada muestra texto para la primera respuesta privada y botones para DMs; **no está verificado** que el primer envío admita botones con esta integración. No inventes ese soporte ni conviertas automáticamente un fallo en otro formato.

Antes de ofrecer el flujo a la audiencia, limita la ejecución a una prueba controlada con publicación, comentario y cuenta evaluadora identificados por el usuario; verifica identidad, conversación, ausencia de respuesta previa y resultado tras cada paso. Sin prueba concluyente, deja la campaña en borrador. No envíes en lote ni programes respuestas en esta fase. Una skill no escucha eventos por sí sola: para continuar tras una selección o automatizar comentarios se necesitaría un mecanismo de recepción/consulta y estado de deduplicación, autorizado aparte. Los botones no justifican repetir enlaces ni eludir límites de Meta.

## Escrituras, errores y reintentos

Antes de escribir, confirma destinatario/objeto, contexto completo, ausencia de acción previa y alcance del playbook. Ejecuta una mutación y verifica el resultado mediante lectura de vuelta o estado documentado.

Ante timeout, respuesta ambigua, error transitorio o desconexión, **no repitas a ciegas**: consulta primero el estado. Reintenta solo si la lectura confirma que la acción no ocurrió; si sigue incierto, detente y escala. Ante rechazo de permisos/token, límite o aviso de Instagram, detente; no eludas controles ni cambies permisos. Conserva evidencia mínima sin secretos.
