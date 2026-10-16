---
trigger: glob
description: "Protección de datos personales y sensibles en la interfaz"
globs: "src/**/*.vue,src/**/*.js"
---

- Minimización: no pidas en formularios ni guardes en el estado más datos personales de los necesarios.
- Enmascara datos sensibles cuando no hace falta mostrarlos completos (ej. documento `****1234`, tarjeta `**** **** **** 1234`, email parcial) reutilizando la utilidad de enmascarado del proyecto en su ubicación real; no presupongas `src/utils/maskData.js`.
- No muestres datos personales en títulos, tooltips, URLs, `document.title` ni en notificaciones.
- Los stores no deben conservar datos personales más tiempo del necesario; límpialos al salir de la vista o al cerrar sesión.
- Autocompletado: en campos sensibles que no deban recordarse usa `autocomplete="off"` o el valor adecuado.
- Cookies/almacenamiento no esenciales (analítica, terceros): no agregues ninguno sin avisarme; puede requerir consentimiento del usuario.
- No envíes datos personales a servicios de terceros (analítica, monitoreo de errores, chats) sin avisarme.
- Capturas, exportaciones o impresiones de datos masivos (CSV, PDF) deben requerir permiso y avisarme para definir su control.
- Si una pantalla muestra datos de varios usuarios, nunca los mezcles en caché compartida entre sesiones.
