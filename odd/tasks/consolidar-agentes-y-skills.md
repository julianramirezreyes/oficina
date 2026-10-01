# Consolidar agentes y definir skills por rol

## Objetivo

Reducir la oficina de 18 a 14 archivos `AGENTS.md` sin perder responsabilidades y documentar cómo asignar skills específicas a cada agente.

## Alcance autorizado

- Reubicar los cuatro orquestadores en el `AGENTS.md` de la raíz de cada departamento.
- Mantener los cuatro gestores de atención y ventas y los dos especialistas de productos digitales.
- Consolidar contenido orgánico en `copy-organico` y `editor-organico`.
- Consolidar publicidad paga en `copy-ads` y `editor-ads`.
- Investigar el descubrimiento de skills y recomendar solo las necesarias; no instalar skills no verificadas ni crear una aplicación.

## Restricciones y criterios de aceptación

- Todas las instrucciones de la oficina permanecen en español neutro.
- Cada especialista tiene una carpeta propia con un `AGENTS.md`; cada departamento tiene un `AGENTS.md` orquestador en su raíz.
- `copy-organico` cubre investigación, ideación, modelado responsable, guiones, copies y entrega en Word al editor.
- El orquestador de publicidad paga conserva planificación y medición de campañas; `copy-ads` conserva concepto creativo y copy; `editor-ads` conserva producción y edición.
- No se crean proyectos o tareas de Codex, no se instalan plugins y no se configura Git sin solicitud expresa.

## Tareas

- [x] **T1 — Reestructurar AGENTS.md.** Ruta: delegada; disparadores: lectura de 18 archivos y escritura de varios archivos no triviales. Verificado: 14 archivos en las rutas previstas, sin referencias a directorios eliminados; revisión independiente de roles y corrección de precedencia de especialistas. Commit: no disponible, porque no existe repositorio Git.
- [x] **T2 — Investigar skills por rol.** Ruta: delegada; disparadores: investigación externa y comparación de documentación actual. Resultado: ubicación y activación verificadas en fuentes oficiales; selección mínima entregable al usuario, sin instalar. Commit: no disponible, porque no existe repositorio Git.

## Verificación y entrega

- Comprobación estructural: `find . -name AGENTS.md -print | sort` y recuento de 14 archivos.
- Comprobación de referencias a nombres de carpetas eliminadas y lectura de los archivos fusionados.
- La tarea solo contiene instrucciones Markdown; no hay ejecutable ni runner de pruebas en esta carpeta. TDD estricto: no aplicable a este cambio documental; origen: instrucciones de la sesión.
- Esta carpeta no es un repositorio Git: no es posible crear una rama, commits de unidad de trabajo ni ejecutar revisión basada en diff de Git. No inicializar Git sin permiso.
- Estrategia de entrega: `ask-on-risk`, sin PR previsto.

## Progreso

- Estado: reorganización e investigación terminadas; no se instalaron skills ni se crearon proyectos o tareas de Codex.
- Evidencia: `find . -type f -name AGENTS.md | wc -l` devolvió `14`; comprobación estructural con `python3` devolvió `PASS`; búsqueda de rutas antiguas sin coincidencias. El primer intento con `python` falló porque ese alias no está instalado; se repitió con `python3`.
- Siguiente paso: elegir una tarea real por especialidad, probar si necesita una skill y después instalar o crear solo la skill necesaria en la carpeta del agente.
