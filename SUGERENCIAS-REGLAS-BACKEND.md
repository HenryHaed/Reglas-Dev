# Sugerencias reglas backend

Fecha: 2026-10-16.

## Propósito y estado

Propuestas para preparar reglas de agentes como Codex, Cursor, Antigravity o Claude en proyectos backend con Node.js, Python y desarrollo de modelos de inteligencia artificial.

Este documento es una guía de mejoras para revisar con el programador. No activa reglas backend, no modifica las reglas frontend y no autoriza instalaciones, migraciones, acceso a producción ni cambios en servicios externos. Esta carpeta contiene un paquete de instrucciones, no un backend que se haya auditado o probado.

El objetivo es producir código seguro, reutilizable y mantenible, con responsabilidades claras, protección de datos y verificaciones reales. Las reglas definitivas deben adaptarse a la arquitectura, versiones y riesgos de cada repositorio.

## 1. Identificar el proyecto antes de intervenir

- Consultar la estructura, documentación, configuración y scripts existentes antes de proponer módulos nuevos.
- En Node.js, comprobar `package.json`, lockfile, versión del runtime, gestor de paquetes y framework utilizado.
- En Python, comprobar `pyproject.toml`, archivos de requisitos o lockfiles disponibles, versión del intérprete y entorno de ejecución real.
- Mantener el framework, ORM, cliente de base de datos, sistema de pruebas y convenciones existentes; no introducir una arquitectura por preferencia del agente.
- Respetar JavaScript o TypeScript según el backend real, sin migrar el lenguaje por iniciativa propia. Las preferencias frontend no determinan el lenguaje del servidor.
- Consultar documentación de la versión utilizada cuando existan dudas de compatibilidad. No imponer herramientas de consulta específicas.
- No instalar, actualizar ni sustituir dependencias o regenerar lockfiles sin autorización expresa.
- Si no hay acceso al repositorio backend, señalar la incertidumbre y evitar inventar endpoints, modelos, tablas o contratos.

## 2. Supervisión del programador y alcance de los cambios

Se propone conservar para el backend la revisión por archivos solicitada por el programador:

- Desde 3 archivos afectados, presentar la lista concreta, cambios previstos, motivo, riesgos y verificaciones; esperar confirmación explícita antes de aplicarlos.
- Si se prevén 3 o más archivos desde el inicio, consultar antes del primero. Si el alcance aumenta durante el trabajo, detenerse antes del tercero.
- Organizar trabajos mayores en lotes de 3 a 4 archivos y confirmar cada lote; el último puede ser menor y también se presenta para aprobación.
- Contar archivos distintos creados, modificados, renombrados o eliminados, incluidos tests, migraciones, configuración y documentación.
- No dividir artificialmente cambios en lotes pequeños para evitar el umbral. Leer archivos y preparar una propuesta no equivale a modificarlos.
- La autorización general de una tarea no sustituye la confirmación del lote concreto; conservar la aprobación del mismo lote mientras no cambie su alcance.
- Solicitar autorización para operaciones destructivas, producción, migraciones de datos, cambios de permisos o contratos públicos, aunque afecten menos de 3 archivos.
- Conservar cambios previos del programador y evitar refactorizaciones ajenas al objetivo.
- Nunca usar credenciales, enviar información a servicios externos ni ejecutar acciones fuera del alcance autorizado por el hecho de disponer de herramientas para hacerlo.

## 3. Reutilización y organización de componentes backend

En backend, los componentes incluyen módulos, servicios, repositorios de datos, validadores, clientes externos, tareas y utilidades.

- Buscar y reutilizar implementaciones existentes antes de crear otra para la misma responsabilidad.
- Separar transporte HTTP, reglas de negocio y persistencia cuando la arquitectura lo permita, sin imponer carpetas o capas innecesarias.
- Mantener controladores o handlers centrados en recibir, validar y coordinar solicitudes, evitando concentrar toda la lógica del sistema en ellos.
- Centralizar políticas de autorización, validación compartida, acceso a servicios externos y manejo de errores.
- Evitar servicios genéricos con muchas banderas o excepciones por consumidor; separar responsabilidades cuando reduzca el acoplamiento.
- No extraer una abstracción únicamente porque dos bloques se parezcan. Evaluar si representan el mismo concepto y cambian por las mismas razones.
- Preservar contratos y revisar consumidores antes de modificar funciones compartidas.
- Documentar entradas, salidas, errores y efectos secundarios cuando no sean evidentes.
- Definir tamaños y complejidad con el programador. El límite de archivos `.vue` no debe trasladarse automáticamente a módulos Node.js o Python.

## 4. Contratos de API y validación en el servidor

- Validar parámetros de ruta, query, cabeceras y cuerpos en el servidor; no confiar en la validación del frontend.
- Comprobar tipos, longitudes, rangos, formatos y campos permitidos con los validadores disponibles.
- Rechazar campos no autorizados y evitar asignar directamente un cuerpo recibido a una entidad persistida.
- Definir métodos, formatos, códigos de respuesta, límites y errores de cada endpoint.
- Retornar únicamente los campos necesarios; no serializar automáticamente entidades con información interna.
- Aplicar paginación y límites a listados, búsquedas, cargas y exportaciones.
- Definir timeouts y límites de solicitudes; no permitir trabajo o consumo sin límite.
- Configurar CORS para los orígenes necesarios y recordar que no sustituye la autorización del servidor.
- Documentar y aprobar cambios incompatibles de contrato antes de implementarlos.

Referencia: [OWASP: seguridad de APIs REST](https://cheatsheetseries.owasp.org/cheatsheets/REST_Security_Cheat_Sheet.html).

## 5. Autenticación, permisos y sesiones

- Reutilizar el mecanismo de autenticación existente; no implementar criptografía ni protocolos propios.
- Denegar por defecto y comprobar permisos en cada operación protegida.
- Verificar acceso al recurso concreto y a la organización correspondiente, no solo si el usuario inició sesión o conoce un identificador.
- Obtener la identidad de un contexto autenticado confiable, no de campos de usuario, rol u organización enviados libremente por el cliente.
- Probar accesos cruzados entre usuarios y organizaciones, incluyendo listados, búsquedas, exportaciones, cachés y descargas.
- Validar expiración y revocación según el mecanismo de sesión. Si se usan JWT, verificar firma, algoritmo permitido, emisor y audiencia cuando correspondan.
- Aplicar protección contra intentos repetidos de acceso y recuperación de cuentas, evitando respuestas que faciliten enumerar usuarios.
- Cuando la autenticación dependa de cookies, configurar sus atributos de seguridad y las defensas CSRF correspondientes.
- Almacenar contraseñas mediante hashing especializado con una biblioteca mantenida; nunca en texto plano ni mediante cifrado reversible para recuperarlas.

Referencia para contraseñas: [OWASP: almacenamiento de contraseñas](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html).

## 6. SQL injection, NoSQL e integridad de datos

- Utilizar consultas parametrizadas para valores; nunca concatenar ni interpolar entradas externas dentro de SQL.
- Revisar consultas crudas y procedimientos almacenados que construyan SQL dinámico, incluso si el proyecto utiliza un ORM.
- Para nombres de columnas, tablas u órdenes que no admitan parámetros de valor, utilizar un mapeo o lista de opciones permitidas.
- No tratar una función genérica de limpieza de texto como sustituto de la parametrización.
- En NoSQL, validar tipos, operadores y estructura de consultas; no aceptar filtros arbitrarios proporcionados por el cliente.
- Usar credenciales con los permisos mínimos necesarios y separar las de ejecución de las de administración o migración.
- Proteger operaciones relacionadas con transacciones y restricciones de integridad en la base de datos.
- Diseñar idempotencia para operaciones que puedan repetirse por reintentos; deshabilitar un botón del frontend no evita duplicados en el servidor.
- Revisar concurrencia, condiciones de carrera y actualizaciones perdidas en operaciones críticas.
- Preparar migraciones con evaluación del impacto, respaldos cuando correspondan y estrategia de recuperación; nunca ejecutarlas en producción sin autorización.

Referencia: [OWASP: prevención de SQL injection](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html).

## 7. Secretos y configuración

- No incluir contraseñas, claves privadas, tokens o credenciales en código, ejemplos, notebooks, tests o documentación.
- Reutilizar el mecanismo aprobado de gestión e inyección de secretos; no crear otro por conveniencia del agente.
- Mantener configuraciones de ejemplo sin valores reales y separar credenciales por entorno, servicio y finalidad.
- Reducir permisos y duración de credenciales cuando el sistema lo permita.
- Establecer procedimientos de rotación y revocación, incluida la respuesta a una credencial expuesta. Eliminarla del archivo no resuelve por sí solo la exposición.
- Evitar imprimir secretos durante depuración, ejecución de comandos, registro de errores o revisión de configuración.
- No desactivar validación de certificados TLS para resolver problemas de conexión.

Referencia: [OWASP: gestión de secretos](https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html).

## 8. Protección de datos durante todo su ciclo de vida

- Clasificar datos y definir quién puede recopilarlos, consultarlos, modificarlos, exportarlos y eliminarlos.
- Recopilar y devolver solo la información necesaria para la finalidad autorizada.
- No usar datos reales de producción en ejemplos, pruebas o entornos de desarrollo sin un proceso aprobado de protección.
- Distinguir enmascarado, seudonimización y anonimización; ocultar parte de un dato no garantiza que deje de identificar a una persona.
- Proteger transporte y almacenamiento según la sensibilidad, con claves administradas separadamente de los datos.
- Acordar plazos de retención y borrado con la organización; incluir temporales, logs, cachés y respaldos según su política.
- Evitar mezclar datos o resultados en caché entre usuarios u organizaciones.
- Autorizar expresamente transferencias a terceros, indicando destinatario, finalidad y datos necesarios; una simple notificación no equivale a permiso.
- Proteger exportaciones y copias de respaldo con permisos, límites y trazabilidad. Comprobar la restauración cuando forme parte del alcance.
- No inventar obligaciones legales o políticas de retención; consultar las decisiones aplicables al proyecto.

## 9. Archivos, comandos y conexiones externas

- Validar archivos en el servidor por tamaño, contenido esperado y tipo permitido; no confiar únicamente en la extensión o MIME declarado.
- Generar nombres internos seguros y resolver rutas dentro de directorios autorizados para impedir acceso fuera de ellos.
- Evitar ejecución de archivos subidos y controlar autorización tanto al subir como al descargar.
- Establecer límites de descompresión, cantidad de archivos y recursos consumidos al procesar documentos o archivos comprimidos.
- Evitar construir comandos de shell con entradas externas. Cuando sea necesario ejecutar un proceso, usar argumentos separados, ejecutables permitidos y límites de tiempo y recursos.
- Restringir destinos de solicitudes salientes para prevenir acceso indebido a redes internas, servicios de metadatos u otros recursos sensibles.
- Comprobar redirecciones y resolución de destinos cuando afecten esas restricciones; limitar tamaño de respuesta y tiempo de conexión.
- En webhooks, verificar autenticidad e integridad con el mecanismo del proveedor, controlar repetición de eventos y aplicar idempotencia.

## 10. Reglas específicas para Node.js

- Respetar la versión de Node.js y el modelo de módulos existentes; no mezclar ESM y CommonJS sin necesidad y revisión.
- Manejar rechazos de promesas y errores asíncronos con el patrón del framework, evitando respuestas duplicadas.
- Evitar operaciones síncronas costosas o trabajos de CPU prolongados en el ciclo de atención de solicitudes; reutilizar workers o colas cuando ya formen parte de la arquitectura.
- Limitar cuerpos de solicitudes, concurrencia y procesamiento de entradas; revisar expresiones regulares que puedan consumir tiempo excesivo.
- Validar claves y estructura al combinar objetos de origen externo para evitar modificaciones de propiedades no permitidas.
- Cerrar correctamente conexiones, pools, streams y procesos durante fallos o apagado del servicio.
- No continuar como si nada tras un fallo fatal que deje el proceso en estado inconsistente; seguir la política de recuperación del servicio.
- Mantener los scripts y herramientas disponibles, sin agregar paquetes por iniciativa propia.

Referencia: [OWASP: seguridad en Node.js](https://cheatsheetseries.owasp.org/cheatsheets/Nodejs_Security_Cheat_Sheet.html).

## 11. Reglas específicas para Python

- Utilizar el entorno aislado y gestor existentes, sin instalar paquetes globalmente.
- Conservar convenciones del framework y reutilizar validación, autenticación y persistencia ya configuradas.
- Usar gestores de contexto o mecanismos equivalentes para cerrar archivos, conexiones y transacciones.
- Evitar excepciones capturadas y silenciadas; manejar casos esperados y registrar fallos de forma segura.
- No bloquear flujos asíncronos con trabajo costoso sin evaluar su ejecución en los mecanismos disponibles.
- No cargar objetos serializados de fuentes no confiables mediante `pickle` ni mecanismos equivalentes capaces de ejecutar código.
- Verificar procedencia e integridad de artefactos antes de cargarlos; una extensión de archivo no acredita seguridad.
- Usar los formateadores, análisis y tests del proyecto. No imponer herramientas o anotaciones nuevas como requisito universal.

La documentación de Python advierte que deserializar datos maliciosos con `pickle` puede ejecutar código. Referencia: [documentación oficial de pickle](https://docs.python.org/3/library/pickle.html).

## 12. Errores, registros y observabilidad

- Centralizar errores con respuestas estables y comprensibles, sin exponer consultas, trazas internas, credenciales o rutas del servidor.
- Conservar detalles técnicos útiles en registros internos protegidos, con acceso y retención definidos.
- No desactivar todos los logs en producción: mantener los eventos operativos y de seguridad necesarios, excluyendo secretos y datos personales innecesarios.
- Utilizar identificadores de correlación para investigar un fallo entre servicios sin registrar cargas completas sensibles.
- Evitar duplicar el mismo error en varias capas sin aportar contexto.
- Registrar cambios relevantes de permisos, operaciones administrativas y accesos sensibles según las políticas del proyecto.
- Definir métricas y alertas útiles de errores, latencia, saturación y abuso; no instalar monitoreo ni enviar telemetría externa sin autorización.

## 13. Pruebas, dependencias y verificación de seguridad

- Reutilizar las herramientas existentes y elegir pruebas según el comportamiento y riesgo del cambio.
- Incluir pruebas unitarias para lógica y pruebas de integración con recursos aislados cuando sean necesarias para verificar persistencia o contratos reales.
- Probar usuarios sin permisos, acceso a recursos ajenos, validaciones inválidas, sesiones expiradas, duplicados y concurrencia en operaciones críticas.
- Incluir casos de consultas maliciosas, archivos fuera de límites y destinos externos no permitidos cuando esas funciones existan.
- Evitar datos, credenciales y servicios de producción; aprobar previamente cualquier prueba con efectos externos.
- No borrar ni debilitar pruebas para obtener resultados favorables; justificar cambios de expectativas por requisitos autorizados.
- Revisar vulnerabilidades de dependencias, secretos expuestos y patrones inseguros mediante las capacidades disponibles; no instalar escáneres automáticamente.
- Verificar procedencia, mantenimiento, licencia y necesidad antes de proponer una dependencia. No ejecutar scripts remotos o de instalación sin revisión y autorización.
- Definir qué hallazgos bloquean una entrega y cómo se aprueban excepciones, con responsable y seguimiento.
- Registrar comandos ejecutados, resultados y limitaciones. Un escaneo sin hallazgos no demuestra ausencia de vulnerabilidades.

## 14. Rendimiento, tareas y operación

- Medir antes de optimizar y relacionar métricas con tiempos de respuesta y carga reales.
- Revisar consultas repetidas, patrones N+1, índices, paginación y tamaños de respuesta antes de añadir cachés o infraestructura.
- Usar pools y límites de concurrencia apropiados; no lanzar trabajo ilimitado para ganar velocidad aparente.
- Definir timeouts, reintentos limitados y condiciones de recuperación; repetir solo operaciones seguras o protegidas mediante idempotencia.
- En tareas de fondo, contemplar duplicados, fallos parciales, cancelación y reanudación según el sistema existente.
- Definir claves, caducidad e invalidación de caché sin romper aislamiento de usuarios ni autorización.
- Separar desarrollo, pruebas y producción. No conectar un entorno de trabajo a producción por defecto.
- Ejecutar servicios con permisos mínimos, aislar recursos y restringir exposición de endpoints administrativos.
- Preparar despliegues y recuperación con configuración verificable, comprobaciones de salud y autorización del programador.

## 15. Desarrollo y operación de modelos de IA

- Verificar origen, licencia, autorización de uso y calidad de datasets y modelos externos.
- Versionar datos, código, configuración, hiperparámetros y artefactos; registrar el entorno y las semillas utilizadas cuando corresponda.
- Separar entrenamiento, validación y prueba, evitando duplicados o información que contamine la evaluación.
- Revisar datos alterados o manipulados que puedan introducir comportamientos no deseados.
- Definir métricas y criterios de aceptación antes de entrenar; conservar un modelo de referencia y evaluar casos relevantes, errores y sesgos.
- Proteger datasets, pesos, resultados y registros con permisos, cifrado y retención adecuados.
- Validar artefactos externos y evitar ejecutar código remoto durante su carga sin revisión y autorización.
- Establecer límites de tiempo, CPU, GPU, memoria y coste; autorizar trabajos costosos antes de iniciarlos.
- Aislar entrenamiento e inferencia, autenticar endpoints y limitar solicitudes y concurrencia.
- Evaluar riesgos de extracción del modelo o exposición de información de entrenamiento.
- Monitorear calidad, latencia y cambios en los datos; permitir retirar una versión y recuperar una anterior.
- Documentar resultados y límites; no declarar reproducibilidad o mejora de precisión sin evidencia.

Referencia: [OWASP: operación segura de modelos de IA](https://cheatsheetseries.owasp.org/cheatsheets/Secure_AI_Model_Ops_Cheat_Sheet.html).

## 16. Documentación y evidencias

- Mantener documentación verificable de arquitectura, servicios, contratos, modelos de datos y configuración, reutilizando los documentos que ya existan.
- Registrar decisiones que afecten permisos, datos, persistencia o contratos públicos, con el motivo y los consumidores afectados.
- Proponer un modelo de amenazas proporcionado: qué se protege, quién puede acceder, por dónde entran los datos y qué fallos tendrían mayor impacto.
- Relacionar controles importantes con verificaciones concretas y responsables, evitando listas que solo declaren intenciones.
- Registrar cambios, pruebas y riesgos pendientes sin inventar evidencia de cumplimiento ISO 27001 u otros estándares.
- Separar resultados ejecutados de recomendaciones y trabajo pendiente; identificar qué depende del backend, infraestructura u organización.
- Actualizar documentación cuando cambie un contrato o una decisión relevante, sin reescribirla por cada ajuste menor.

## 17. Organización sugerida para un futuro paquete de reglas

| Grupo | Contenido propuesto |
| --- | --- |
| Base común | Alcance, confirmación del programador, reutilización, versiones y evidencias. |
| Node.js | Runtime, asincronía, framework, recursos y errores. |
| Python | Entorno, framework, manejo de recursos y deserialización. |
| APIs y permisos | Contratos, validación, autenticación, autorización y límites. |
| Persistencia | SQL/NoSQL, integridad, transacciones, concurrencia y migraciones. |
| Datos y secretos | Clasificación, accesos, cifrado, retención, exportación y credenciales. |
| Calidad y operación | Pruebas, dependencias, observabilidad, rendimiento y recuperación. |
| Modelos de IA | Datos, entrenamiento, evaluación, artefactos e inferencia. |

Mantener una fuente común de contenido y adaptaciones de formato por agente. Verificar cómo se cargan las instrucciones en la versión y configuración de cada herramienta; no suponer que todas interpretan igual los mismos archivos. Activar solo los grupos pertinentes al backend real.

## 18. Orden recomendado de adopción

1. Acordar alcance, arquitectura real, revisión del programador y tratamiento de datos.
2. Incorporar validación, autorización por recurso, parametrización de consultas y manejo de secretos.
3. Añadir contratos, pruebas negativas, trazabilidad y controles de archivos y conexiones.
4. Mejorar reutilización y rendimiento a partir de problemas observados.
5. Incorporar el perfil de modelos de IA solo si existe esa actividad en el proyecto.

Cada etapa debe terminar con cambios revisables, pruebas pertinentes y limitaciones explícitas. Adoptar estas propuestas requiere una tarea posterior autorizada; la creación de este documento no implementa controles en un backend.
