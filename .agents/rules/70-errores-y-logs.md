---
trigger: glob
description: "Manejo de errores y registro seguro en el frontend"
globs: "src/**/*.vue,src/**/*.js"
---

- Reutiliza el manejo de errores existente, incluido el global cuando exista; no añadas handlers duplicados ni reestructures el sistema por un ajuste visual.
- Mensajes al usuario: seguros, breves y orientados a continuar ("No se pudieron guardar los cambios. Inténtalo de nuevo"). Nunca muestres stack traces, SQL, rutas ni el mensaje crudo del backend.
- Distingue los errores: 401 (sesión), 403 (sin permiso), 404, 422 (validación, mostrando solo mensajes de campo seguros), 5xx (genérico).
- Si el proyecto envía errores a un servicio de monitoreo (Sentry, etc.): no envíes tokens, contraseñas ni datos personales; filtra el payload. Si no existe, no lo agregues como parte de una tarea visual.
- Prohibido `console.log` de datos sensibles. Usa un wrapper central de logging que se silencia en producción.
- Cada error de API debería poder rastrearse: si el backend devuelve un `requestId`, muéstralo o regístralo para soporte (sin exponer detalles internos).
- Contempla carga, vacío, éxito y error cuando correspondan; conserva los datos permitidos del formulario ante errores recuperables y evita notificaciones duplicadas. Aplica la regla 85.
