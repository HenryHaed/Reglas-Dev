# Reglas del frontend institucional (Codex y OpenCode)

Estas instrucciones aplican al FRONTEND de este repositorio; no se deben imponer al backend.

## Obligaciones de documentación
- Es OBLIGATORIO disponer de `docs/ESTRUCTURA.md` y `docs/COMPONENTS.md`. Antes de modificar código, comprueba su existencia y consúltalos.
- Si falta alguno, inspecciona el repositorio y créalo automáticamente con información verificable; no inventes rutas, archivos, props ni componentes. Si el usuario pide solo análisis, no crees ni modifiques archivos.
- Si existen, verifica las secciones relacionadas con la tarea y actualízalas cuando cambie estructura o contratos. Reutiliza lo ya comprobado; no repitas todo el inventario por cada edición cosmética.
- Para crear `docs/ISO-EVIDENCIAS.md`, `README.md` u otros documentos nuevos, solicita autorización si no está ya incluida en la petición. Esa autorización no sustituye la confirmación del lote de archivos de la regla 30; conserva la confirmación ya dada al mismo lote. `AGENTS.md` se entrega como parte de la configuración del agente.

## Compatibilidad y versiones: prioridad por repositorio
- Consulta `package.json`, lockfile y configuración real de Vue, Vuetify, Vite, Pinia, gráficos e iconos cuando afecten la tarea.
- Las versiones mencionadas en ejemplos o proyectos anteriores NO determinan las versiones de este repositorio.
- Aplica APIs y patrones compatibles con la versión existente. No impongas Vuetify 3 ni Vuetify 4.
- No instales, actualices ni migres paquetes ni modifiques lockfiles sin autorización expresa. Si hay una incompatibilidad, intenta la adaptación de menor impacto y explica riesgos antes de proponer migraciones.

## Estándar visual institucional obligatorio
- En los componentes, secciones o flujos nuevos o modificados del alcance autorizado, aplica los tokens y patrones institucionales. Un ajuste local no autoriza rediseñar toda la pantalla.
- Usa `designSystem.js` y los archivos maestros proporcionados como referencia, comprobando qué existe en el repositorio antes de integrarlo; si faltan y no fueron proporcionados, solicita los archivos oficiales.
- Se exige el resultado visual y funcional, NO copiar incondicionalmente archivos ni migrar las librerías. Conserva las pantallas ajenas a la tarea.
- Si los materiales discrepan entre paleta petróleo/turquesa e índigo/violeta o Urbanist e Inter, prioriza la paleta institucional aprobada y solicita decisión para cambios globales.
- Verifica accesibilidad, contraste, temas y regresiones en lo que se modifique; no afirmes pruebas que no se hayan ejecutado.

## UX/UI y CSS sin nuevas dependencias
- Diseña interfaces claras para personas sin conocimientos técnicos: propósito reconocible, acción principal por tarea, textos breves y detalles secundarios bajo demanda.
- Conserva visibles los datos esenciales, errores y consecuencias; simplifica sin ocultar información necesaria.
- Personaliza en este orden: props/slots disponibles, tema/tokens/defaults existentes, clases compartidas, CSS local scoped y `:deep()` acotado como último recurso.
- Usa Vue, Vuetify y CSS nativo disponibles. No instales herramientas, fuentes, iconos, frameworks CSS ni dependencias para mejoras visuales.
- Verifica móvil, escritorio, teclado, foco, temas existentes y estados de carga/vacío/éxito/error afectados; reporta las limitaciones reales.

## Desarrollo eficiente y componentes
- Entre 150 y 300 líneas revisa si conviene dividir; 150 no es un mínimo. El máximo es 300 líneas físicas por archivo `.vue` nuevo o reorganizado, incluyendo template, script y estilos. Componentes menores son válidos por mantenimiento.
- Divide por responsabilidades antes del máximo; no comprimas código para eludirlo. En heredados que ya lo superen, informa el conflicto y aplica solo extracciones dentro del alcance; no declares cumplimiento sin resolverlo.
- Reutiliza por responsabilidad y contrato, sin extracción automática en la segunda repetición ni obligación de crear stores para estado local.
- Confirmación obligatoria desde 3 archivos: presenta al programador la lista de archivos, cambios, motivos, riesgos y verificaciones, y espera su confirmación explícita antes de editar. Aplica también a CSS, textos, documentación y archivos auxiliares.
- Si prevés 3 o más archivos, consulta antes del primer cambio; si el alcance crece, detente antes del tercero. Para trabajos mayores, presenta lotes de 3 a 4 archivos y solicita confirmación antes de cada lote, incluido el último aunque sea menor.
- Cuenta todos los archivos distintos afectados en la tarea, incluidas las copias para otros agentes. No dividas cambios en lotes de 1-2 archivos para eludir el umbral ni decidas por el programador; mientras falte confirmación, limita el trabajo a inspección y preparación de propuestas.
- La autorización general de una tarea no sustituye la confirmación del lote concreto. Conserva la confirmación ya dada al mismo lote; si cambian sus archivos o alcance, consulta de nuevo. Los cambios sensibles pueden requerir confirmación incluso con 1 o 2 archivos, según la regla 30.
- Consulta documentación cuando haya dudas de API o compatibilidad; Context7/MCP son opcionales. Reutiliza patrones ya verificados.
- Agrupa verificaciones pertinentes; no repitas builds por cada ajuste ni añadas tests que solo reproduzcan CSS. Nunca reduzcas controles de seguridad por rapidez.

## Seguridad y mantenimiento
- Reutiliza módulos, componentes, stores, servicios, rutas y convenciones del proyecto. No presumas carpetas de Gaceta, Paperless o MOF.
- JavaScript y Composition API `<script setup>` cuando el proyecto use Vue 3; no introduzcas TypeScript por iniciativa propia.
- Mantén las protecciones de acceso, rutas y manejo de datos en frontend; recuerda que el servidor debe validar los permisos y entradas.
- No inventes evidencias de conformidad ISO 27001; documenta únicamente cambios y pruebas reales.
- No realices refactorizaciones masivas ni cambies dependencias sin autorización.

## Referencia detallada
- Las reglas canónicas de este paquete están en `.cursor/rules/*.mdc` y sus equivalentes de Antigravity en `.agents/rules/*.md`.
- Consulta solo las reglas relevantes: 00 contexto/documentación; 05 reutilización; 10 componentes/tamaño/rendimiento; 20 y 50 seguridad; 30 confirmación desde 3 archivos/verificación; 40 evidencias; 60 privacidad; 70 errores; 80 pruebas; 85 UX/UI; 90 identidad/CSS; 100 compatibilidad; 110 integración de recursos oficiales.
- Los patrones de activación son ayudas: verifica el módulo frontend real y no apliques estas instrucciones a JavaScript de backend. En monorepositorios, acota los patrones al frontend al configurar el paquete.
- Mantén equivalentes los cuerpos de Cursor y Antigravity; cambia únicamente sus metadatos específicos. En Codex/OpenCode, este archivo es el punto de entrada.
