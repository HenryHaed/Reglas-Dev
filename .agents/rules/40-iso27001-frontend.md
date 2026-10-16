---
trigger: always_on
description: "Cumplimiento ISO/IEC 27001:2022 (Anexo A) aplicado al desarrollo frontend"
---

Este proyecto busca alinearse con ISO/IEC 27001:2022. Al generar o modificar código frontend, aplica estos controles
(la referencia al control del Anexo A va entre paréntesis para trazabilidad).

# Control de acceso (A.5.15, A.8.2, A.8.3)
- Las rutas protegidas usan guards del router (`beforeEach`) que verifican autenticación y rol/permiso.
- Ocultar o deshabilitar un botón o menú NO es seguridad: es solo UX. El permiso real lo valida el backend; asume siempre que puede responder 401/403 y manéjalo (redirigir a login o mostrar mensaje genérico).
- Los permisos se leen desde un único lugar (store o composable, ej. `usePermissions`), no repartidos por componentes.
- Nunca incluyas usuarios, roles o credenciales de prueba en el código.

# Autenticación y sesión (A.8.5)
- Sesión con expiración: al recibir 401, limpia el estado de sesión y redirige a login.
- Logout limpia stores, caché y cualquier dato de usuario en memoria.
- Inactividad: si el proyecto lo requiere, implementa cierre de sesión por inactividad (avísame antes de definir el tiempo).
- Formularios de contraseña: `type="password"`, `autocomplete` correcto, sin mostrar ni registrar el valor.

# Desarrollo seguro (A.8.25, A.8.26, A.8.28)
- Todo código nuevo debe considerar: validación de entrada, manejo de errores, estados de carga/error y permisos.
- Usa OWASP Top 10 como referencia en el cliente (XSS, control de acceso roto, componentes vulnerables, configuración insegura).
- Código crítico (login, permisos, formularios con datos personales, pagos) debe tener tests (ver 80-testing-frontend).
- No uses datos reales de producción en ejemplos, mocks, fixtures ni comentarios.

# Gestión de dependencias y vulnerabilidades (A.8.8, A.5.21, A.5.22)
- Las tareas visuales no autorizan dependencias nuevas. En una tarea separada de dependencias, toda incorporación requiere autorización y justificación de mantenimiento, necesidad y alternativas existentes.
- Al agregar o actualizar paquetes, sugiere correr `npm audit`.
- Mantén el lockfile versionado; no uses `latest` ni rangos abiertos en dependencias críticas.
- No cargues scripts, estilos ni fuentes de CDNs externos para una mejora visual. Cualquier integración externa requiere autorización expresa y las protecciones aplicables, incluido SRI cuando sea compatible.

# Separación de entornos (A.8.31)
- URLs y configuración por entorno vía `.env.development`, `.env.production`, etc. Nunca apuntes a producción desde desarrollo.
- Mantén `.env.example` actualizado y sin valores reales. Nunca subas `.env` al repositorio.
- Las herramientas de debug (devtools, logs verbosos, mocks) deben quedar desactivadas en el build de producción.

# Gestión de cambios (A.8.32)
- Cambios de funcionamiento en autenticación, permisos, tratamiento de datos personales o dependencias críticas: explica impacto y aplica la autorización de la regla 30. Ajustar CSS o textos conserva esos controles, pero sigue exigiendo confirmación del programador desde 3 archivos según la regla 30; no se excluyen los cambios visuales del umbral.
- Si el cambio es relevante para auditoría (auth, permisos, datos personales, dependencias críticas, configuración de seguridad), registra la evidencia real en `docs/ISO-EVIDENCIAS.md` con fecha, cambio, motivo, control ISO y verificación. Si falta el documento, solicita autorización antes de crearlo y reporta el registro pendiente.

# Qué NO debes asumir
- No declares que el código "cumple ISO 27001" por sí solo: indica qué controles cubre el cambio y cuáles dependen del backend, la infraestructura o políticas de la organización.
- Si algo requiere una decisión de la organización (tiempo de inactividad, política de retención, clasificación de datos), pregúntame en vez de inventarlo.
