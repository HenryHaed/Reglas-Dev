---
trigger: always_on
description: "Reglas generales del proyecto (contexto, flujo de trabajo y dependencias)"
---

# Contexto y alcance
- Estas reglas son exclusivamente del frontend. Detecta el módulo real antes de aplicarlas: un archivo JavaScript o un package.json también puede pertenecer al backend.
- En proyectos Vue 3 usa JavaScript y Composition API con `<script setup>`; conserva las versiones y librerías existentes. No introduzcas TypeScript, Pinia, Vite ni herramientas ausentes.
- Para mejoras visuales utiliza Vue, Vuetify y CSS nativo disponibles; no instales ni actualices paquetes, fuentes, iconos o herramientas adicionales.
- Comprueba los alias de importación en la configuración real; no presupongas que `@` existe o apunta a `src/`.
- Responde en español; sigue las convenciones existentes para identificadores y comentarios.

# Documentación obligatoria
- Antes de implementar, comprueba y consulta `docs/ESTRUCTURA.md` y `docs/COMPONENTS.md`; contrasta con el código las secciones relacionadas con la tarea.
- Si faltan, inspecciona el repositorio y créalos automáticamente con información verificable. No generes archivos en una tarea expresamente limitada a análisis o lectura.
- `ESTRUCTURA.md` describe carpetas, módulos, rutas y configuración reales. `COMPONENTS.md` registra componentes reutilizables, rutas y props, emits y slots verificables.
- No inventes estructuras ni contratos. Si solo existe un paquete de reglas, documenta ese alcance y la ausencia de componentes ejecutables.
- Conserva contenido válido; actualiza estructura o contratos cuando el cambio los afecte. Un ajuste de texto, color o espaciado no exige cambios documentales si no altera esos datos.
- Reutiliza la información ya comprobada durante la tarea. Relee si cambia el contexto, los archivos relevantes o hay indicios de desactualización; no repitas una inspección completa por cada edición.
- Si falta acceso, informa el bloqueo y continúa lo que pueda verificarse; no declares completada documentación inaccesible.

# Creación de otros documentos
- `docs/ISO-EVIDENCIAS.md`: para cambios relevantes de seguridad sigue la regla 40; si falta, solicita autorización para crearlo y comunica la evidencia pendiente.
- Para crear o reemplazar `AGENTS.md`, crear `README.md` u otros documentos nuevos, solicita autorización cuando la petición del usuario no la incluya ya. La autorización para crear un documento no sustituye la confirmación del lote de archivos exigida por la regla 30; conserva la confirmación ya dada al mismo lote.
- La autorización documental no permite inventar pruebas ni modificar áreas ajenas a la tarea.

# Trabajo eficiente
1. Identifica el objetivo del usuario, el componente o flujo afectado y los recursos reutilizables.
2. Comprueba versiones declaradas y resueltas en package.json y lockfile cuando afecten a la implementación. Usa el gestor y scripts reales.
3. Consulta documentación oficial de esa versión, documentación local o código instalado cuando haya dudas de API o compatibilidad. Context7 y los MCP son opcionales si están disponibles; no los instales ni los conviertas en un bloqueo.
4. Reutiliza patrones ya verificados en el proyecto. Si no puedes confirmar una API nueva, usa una alternativa conocida compatible o comunica la limitación.
5. Antes de editar, estima los archivos afectados y aplica siempre la regla 30: desde 3 archivos presenta el lote al programador y espera confirmación explícita. Los detalles visuales pequeños no eximen de este umbral; si aumenta el alcance, consulta de nuevo.

# Principios y dependencias
- Código legible, responsabilidades claras y reutilización con criterios de la regla 05.
- Documenta parámetros y retornos de utilidades, servicios y stores cuando ayude a entender contratos; evita comentarios que repitan el código.
- No dejes logs de depuración, código comentado ni imports sin usar.
- No ejecutes instalaciones, actualizaciones, migraciones ni cambios de lockfiles para resolver tareas visuales. Si una función exige otra dependencia, ofrece una alternativa con lo disponible y comunica el límite.
- Ejecuta revisiones de versiones como `npm outdated` solo si se solicitan o forman parte de una tarea autorizada de dependencias; no al inicio de cada trabajo visual.
- Cualquier mantenimiento de dependencias requiere autorización expresa separada del ajuste visual; no apliques `audit fix` automáticamente.
- Verificación y reporte: regla 30; pruebas y revisión visual: regla 80; UX/UI: regla 85; identidad y CSS: regla 90.
