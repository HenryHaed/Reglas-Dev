---
trigger: always_on
description: "Reglas de seguridad obligatorias para el frontend (rutas admin, cargas de archivos, vista previa, API)"
---

# Secretos y configuración
- Nunca hardcodees secretos, tokens, API keys, credenciales ni URLs internas de servidores. Usa variables de entorno.
- Todo lo que empiece con `VITE_` queda público en el navegador: nunca pongas secretos ahí.
- No toques `.env` ni los archivos de despliegue.

# Rutas y área de administración
- Identifica las rutas internas en el router real. No quites ni debilites guards existentes; si una ruta interna carece de protección, informa el hallazgo antes de replicar ese patrón.
- Los guards del frontend son solo una capa de UX: la autorización real debe validarla el backend. Nunca confíes en datos de rol o permiso guardados en el cliente.
- Tokens de sesión: preferir cookies httpOnly; no guardes datos sensibles en `localStorage` ni `sessionStorage`. Nunca pongas tokens en la URL ni en query params.

# Contenido dinámico y XSS
- Prohibido `v-html` con contenido dinámico, salvo sanitización con una solución segura ya instalada y aprobación del uso de HTML. Si no existe, muestra texto escapado o nodos de plantilla; no instales paquetes para una mejora visual.
- Prohibido `eval`, `new Function` e `innerHTML`.
- Funciones de resaltado de coincidencias de búsqueda (`src/utils/`): si generan HTML, deben escapar primero el texto original y la consulta del usuario antes de envolver coincidencias. Preferible renderizar con nodos/plantilla en vez de `v-html`.
- Los datos que vienen de la API (títulos, descripciones, nombres de documentos) se tratan como no confiables.

# Carga de archivos y vista previa
- En cargas de documentos valida en el cliente tipo (extensión y MIME), tamaño máximo y nombre del archivo, y asume que el backend también valida.
- No renderices contenido de archivos subidos como HTML. Para vista previa de PDF u otros usa blob URLs o `iframe`/`object` con origen controlado, y revoca las URLs con `URL.revokeObjectURL` al terminar.
- No construyas URLs de descarga o vista previa concatenando entradas del usuario sin codificar (`encodeURIComponent`).

# API y errores
- Valida formato, tipo y límites con las reglas existentes; escapa la salida según su contexto y sanitiza solo contenido HTML autorizado. No alteres indiscriminadamente lo escrito ni consideres la validación del cliente una defensa suficiente del servidor.
- Maneja errores de API con try/catch y muestra mensajes genéricos al usuario; no expongas stack traces, URLs internas ni detalles del servidor.
- No imprimas datos sensibles ni respuestas completas de la API en `console.log`.
- Reutiliza los clientes HTTP, orígenes y prefijos verificados del proyecto; no eludas sus controles de sesión, errores y timeout mediante llamadas paralelas.

# Dependencias
- Si una dependencia parece insegura, abandonada o innecesaria, avísame antes de instalarla.
- Cuando yo lo pida, ejecuta `npm audit` y resume los hallazgos sin aplicar `npm audit fix` automáticamente.

# Vulnerabilidades en código existente
- Si ves una vulnerabilidad en código que no estás modificando, avísame con archivo y línea al final de tu respuesta, pero no la cambies sin permiso.
