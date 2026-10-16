# Mejoras implementadas en las reglas frontend

Fecha: 2026-10-16.

## Alcance y autorización

Se actualizaron las instrucciones para desarrollo frontend con Vue, Vuetify y CSS, según la petición del usuario. También se autorizó este documento explicativo. No se amplió el paquete a backend, Python ni entrenamiento de modelos de IA.

Los cambios se aplican a las reglas del agente. Esta carpeta no contiene una aplicación ejecutable: no se implementaron pantallas, no se midió rendimiento de una interfaz y no se instalaron paquetes, fuentes, iconos ni herramientas.

## 1. Componentes entre 150 y 300 líneas

Antes, la regla recomendaba dividir al superar aproximadamente 150 líneas. Ahora:

- Entre 150 y 300 líneas se revisan responsabilidad, complejidad, contratos y facilidad de mantenimiento.
- 150 no es un mínimo ni exige dividir automáticamente. Un componente puede ser menor si resulta más claro.
- El máximo es 300 líneas por archivo `.vue` nuevo o reorganizado dentro del alcance.
- Se cuentan todas las líneas físicas: template, script, estilos, comentarios y líneas en blanco.
- Se extraen responsabilidades coherentes antes de superar el máximo; no se permite comprimir código o trasladar bloques sin sentido para cumplir una cifra.
- Los componentes heredados que ya superen 300 líneas se identifican y se tratan mediante extracciones localizadas cuando estén autorizadas. Si resolverlos exige una refactorización amplia fuera del alcance, se informa el conflicto y el trabajo pendiente; no se afirma cumplimiento ni se modifica todo el módulo.
- Las extracciones conservan props, emits, slots y consumidores.

Fuente principal: regla 10. Resumen de acceso rápido: `AGENTS.md`.

## 2. Trabajo del agente con menos interrupciones

- Se elimina el umbral de 3-4 archivos como motivo automático para pedir confirmación.
- Los ajustes pequeños, reversibles y autorizados de CSS, textos, estados y componentes se realizan directamente.
- La confirmación depende de nuevos impactos: contratos incompatibles, arquitectura, identidad global, dependencias, seguridad sensible, operaciones destructivas o despliegues.
- No se repiten permisos ya concedidos.
- Se pueden crear subcomponentes y archivos auxiliares necesarios siguiendo la estructura existente, sin solicitar permiso por cada archivo.
- Una corrección visual local no obliga a rediseñar la pantalla completa.
- Se preserva el trabajo del usuario y se mantienen las restricciones sobre cambios ajenos al alcance.

Fuentes: reglas 05 y 30; ajustes coherentes en 40, 90, 100 y 110.

## 3. Documentación y consultas proporcionales

- Se conserva la obligación de consultar y mantener `docs/ESTRUCTURA.md` y `docs/COMPONENTS.md`.
- Se revisan las secciones relacionadas con la tarea y se reutiliza lo ya verificado mientras siga vigente.
- Se actualiza documentación cuando cambia la estructura o un contrato; un ajuste cosmético sin ese impacto no requiere cambios documentales.
- Las peticiones de solo análisis no crean ni modifican archivos.
- Context7 y los MCP pasan a ser medios opcionales; se admite documentación oficial de la versión real, documentación local y código instalado.
- Se consulta ante dudas de API o compatibilidad, sin repetir consultas por cada propiedad ya comprobada.
- Las revisiones de versiones como `npm outdated` dejan de ejecutarse por iniciar una tarea visual grande.
- Las reglas 00 y 30 concentran el flujo general, y las demás las referencian.

## 4. Reutilización y organización

- Se sustituye la extracción obligatoria en la segunda repetición por una evaluación de responsabilidad y contrato.
- Se evitan componentes genéricos con numerosas banderas y excepciones, así como envoltorios de Vuetify sin valor añadido.
- El estado local permanece local; un store se utiliza para estado compartido o por la arquitectura real.
- Se conserva el uso de clientes HTTP existentes sin imponer un nuevo store o cliente.
- Se eliminan las prescripciones de carpetas, alias y clientes de otros proyectos, como Gaceta/Paperless.
- Se verifican las ubicaciones de validadores y utilidades de privacidad.
- Los patrones de Vue se acotan a archivos `.vue`; el punto de entrada recuerda consultar la regla cuando se modifiquen módulos frontend relacionados y verificar el contexto en monorepositorios.

## 5. Nueva regla 85: UX/UI e interacción sencilla

Se incorpora una regla equivalente en Cursor y Antigravity para:

- Mostrar qué contiene la pantalla, qué puede hacer la persona y qué ocurrió tras actuar.
- Mantener un propósito principal por sección y una acción dominante por tarea.
- Priorizar información necesaria y ofrecer detalles secundarios bajo demanda.
- No esconder errores, consecuencias ni información esencial para reducir contenido.
- Usar lenguaje claro para personas sin conocimientos técnicos, con respeto y sin jerga interna.
- Escribir botones concretos: "Guardar cambios", "Crear usuario" o "Descargar PDF".
- Mantener etiquetas visibles; los placeholders y tooltips no sustituyen información necesaria.
- Agrupar formularios por propósito, partir de una columna y validar sin mostrar errores prematuros.
- Conservar lo escrito ante fallos recuperables, sin persistir secretos.
- Simplificar tablas y filtros, manteniendo acceso al detalle y a los datos esenciales en móvil.
- Diferenciar ausencia de registros de búsquedas sin coincidencias.
- Evitar diálogos anidados y confirmaciones triviales; conservar el foco y explicar acciones destructivas.
- Evitar estadísticas inventadas, contenido de relleno y decoración que no aporte a la tarea.

## 6. CSS y mejora visual de Vuetify

La regla 90 establece este orden:

1. Props, slots y utilidades públicas compatibles.
2. Tema, tokens y defaults existentes, controlando su impacto compartido.
3. Clases maestras para patrones comunes.
4. CSS local con `<style scoped>`.
5. `:deep()` acotado bajo una clase propia como último recurso.

También se añaden criterios de:

- CSS nativo, sin instalar Sass, Tailwind, animaciones, iconos, fuentes u otros paquetes.
- Selectores cortos, sin dependencia innecesaria de la estructura interna de Vuetify.
- Uso excepcional y justificado de `!important`.
- Reutilización de tokens reales sin inventar nombres ni valores institucionales.
- Alcance controlado en menús, diálogos y contenido superpuesto.
- Distribución con grid/flex, adaptación al contenido y ausencia de recortes por alturas fijas.
- Espaciado, alineación y tipografía consistentes; decoración moderada.
- Estados de foco, selección, hover, error y deshabilitado distinguibles.
- Transiciones discretas y respeto a `prefers-reduced-motion`.

Se conservan la paleta y semántica institucionales: petróleo, turquesa, coral, acciones destructivas identificables, tokens oficiales y recursos maestros. No se añadieron archivos maestros ficticios.

## 7. Rendimiento sin dependencias adicionales

- Evitar peticiones duplicadas y cálculos costosos repetidos en el renderizado.
- Usar `computed` y watchers según su responsabilidad.
- Cancelar peticiones anteriores o ignorar respuestas obsoletas cuando corresponda.
- Usar paginación en listas grandes y considerar virtualización solo si ya está disponible, es compatible y conserva accesibilidad.
- Mantener carga diferida cuando aporte valor, sin convertir todos los componentes en asíncronos.
- Liberar timers, listeners, suscripciones y URLs de objeto.
- Medir con herramientas disponibles antes de introducir optimizaciones complejas.

Son requisitos para trabajos futuros: no se afirma una mejora medida de velocidad en este paquete.

## 8. Pruebas, accesibilidad y controles conservados

- Se agrupan verificaciones tras cambios coherentes; se repiten por cambios relevantes, fallos o dudas pendientes.
- Se ejecutan scripts reales disponibles; no se presupone npm ni se instala infraestructura de prueba.
- Los cambios cosméticos se revisan visualmente y mediante interacción, sin tests que solo repitan clases CSS.
- Se mantienen pruebas relevantes para lógica, formularios, permisos, sesión y contratos.
- Se comprueban móvil, escritorio, zoom, textos largos, teclado, foco, temas existentes y estados afectados.
- No se agregan temas para completar una revisión ni se exige crear cinco temas donde no existen.
- Se distinguen verificaciones ejecutadas, pendientes y no aplicables.
- Se conservan controles de XSS, secretos, privacidad, rutas y manejo seguro de errores. La rapidez no permite debilitarlos.
- Si no existe sanitizador seguro, se usa texto escapado o plantilla en lugar de instalar una dependencia para mostrar HTML.
- Ajustar CSS de una pantalla sensible no se confunde con modificar su autenticación o tratamiento de datos.
- Los errores ofrecen una salida útil sin mostrar detalles internos ni duplicar notificaciones.

## Archivos modificados y creados

Cada regla de la tabla tiene una versión `.cursor/rules/<nombre>.mdc` y otra `.agents/rules/<nombre>.md`.

| Regla | Cambio |
| --- | --- |
| 00-general | Alcance frontend, documentación proporcional, consultas y dependencias. |
| 05-codigo-existente | Reutilización por responsabilidad, estado local y estructura real. |
| 10-vue-vuetify | Límite 150-300, mantenimiento, rendimiento y compatibilidad. |
| 20-seguridad | Rutas/clientes reales, validación contextual y HTML sin nuevas dependencias. |
| 30-edicion-codigo | Autonomía, autorización por impacto y verificación proporcional. |
| 40-iso27001-frontend | Diferencia entre cambios visuales y cambios de seguridad; sin recursos externos para diseño. |
| 50-seguridad-frontend-extra | Clientes y validadores existentes; coherencia de restricciones de HTML. |
| 60-privacidad-datos | Ubicación real de la utilidad de enmascarado, sin imponer una ruta. |
| 70-errores-y-logs | Reutilización de handlers, mensajes útiles y estados de interfaz. |
| 80-testing-frontend | Pruebas por riesgo, revisión visual y activación en componentes. |
| 85-ux-ui-frontend | Nueva regla de claridad, contenido, interacción y comodidad. |
| 90-design-system-mof | Orden de personalización, CSS mantenible e identidad dentro del alcance. |
| 100-compatibilidad-versiones-frontend | Diseño sin instalaciones, alcance local y referencias coherentes. |
| 110-integracion-visual-mof | Integración de recursos existentes y verificación proporcional. |

Además:

- `AGENTS.md`: actualizado como punto de entrada e índice temático.
- `README.md`: actualizado con alcance, tamaño de componentes, uso en monorepositorios y enlaces documentales.
- `docs/ESTRUCTURA.md`: creado porque faltaba, describiendo el paquete real.
- `docs/COMPONENTS.md`: creado porque faltaba, declarando la ausencia de componentes ejecutables.
- `docs/MEJORAS-FRONTEND.md`: este registro, creado por solicitud expresa.

## Verificación de esta modificación

Comprobaciones ejecutadas el 2026-10-16:

| Comprobación | Resultado |
| --- | --- |
| Inventario final | 33 archivos: 28 reglas, 2 puntos de entrada/documentación raíz y 3 documentos en docs. Todos son `.md` o `.mdc`. |
| Cuerpos Cursor/Antigravity | Los 14 pares coinciden exactamente. |
| Metadatos | 14 encabezados equivalentes: descripción, patrón y correspondencia entre `alwaysApply` y `trigger`. |
| Contenido escrito | Los archivos de reglas de Cursor, AGENTS, README y el informe coinciden con el contenido preparado. |
| Reglas anteriores incompatibles | No se encontraron las instrucciones anteriores de dividir al superar unas 150 líneas, extraer en la segunda repetición, confirmar por superar 3-4 archivos, imponer el flujo por store o asumir el alias `@`. |
| Consultas y revisión de versiones | No se encontraron las instrucciones anteriores de exigir Context7 siempre ni ejecutar `npm outdated` al comenzar una tarea grande. |
| Enlaces del README | Los 3 enlaces a documentos locales resuelven a archivos existentes. |
| Referencias numeradas | Todas las referencias comprobadas con el formato «regla N» tienen una regla correspondiente. |
| Integridad textual | No se encontraron marcadores de conflicto ni caracteres de reemplazo de codificación en los archivos revisados. |
| Documentos obligatorios | Se consultaron los dos documentos creados y corresponden al paquete sin componentes ejecutables. |

No aplica ejecutar build, lint ni pruebas de interfaz: esta carpeta no contiene `package.json`, scripts ni una aplicación Vue. No se verificó la activación real de las reglas dentro de Cursor o Antigravity; la comprobación de sus metadatos es estática. Tampoco se declara conformidad ISO/WCAG ni pruebas con usuarios.
