---
trigger: glob
description: "Integración obligatoria y compatible del estándar visual institucional con tokens, temas, Vuetify, CSS, gráficos y fuentes"
globs: "src/**/*.vue,src/**/*.js,src/**/*.css,src/**/*.scss,index.html,package.json"
---

# Objetivo obligatorio y alcance
- Implementa el estándar visual en los componentes, secciones o flujos autorizados según la regla 90, con la UX/UI de la regla 85. No amplíes un cambio local a toda la pantalla.
- No te limites a citar los archivos de referencia: adapta e integra su funcionalidad donde corresponda y comprueba que el resultado se renderice.
- Conserva el comportamiento de negocio y las vistas ajenas al alcance; ante cambios masivos, presenta un plan gradual y pide autorización.
- El nombre MOF identifica el origen de los recursos maestros, NO obliga a renombrar el sistema receptor, sus carpetas ni sus módulos.

# Prioridad entre recursos maestros (decisión de integración)
- Toma como fuente principal de paleta institucional los tokens de la versión más reciente suministrada de `designSystem.js`: petróleo, turquesa, coral, fondos, navegación, tablas, textos y variantes `LIGHT_THEME_TOKENS`/`DARK_THEME_TOKENS`.
- Usa `themes.js` para conservar los identificadores `light`, `dark`, `protanopia`, `deuteranopia` y `tritanopia`, y su configuración de accesibilidad; alinea los colores generales de `light` y `dark` con `designSystem.js`, evitando que índigo/violeta sustituyan petróleo/turquesa en esos dos temas.
- Conserva las paletas diferenciadas de protanopia, deuteranopia y tritanopia cuando permitan distinguir mejor los estados; verifica sus contrastes y no afirmes accesibilidad por su nombre.
- Usa el CSS maestro institucional para la semántica de componentes; incorpora de `style (1).css` solo utilidades y selectores compatibles, comprobando duplicidades, especificidad y estados de tema.
- Usa Urbanist como tipografía institucional de referencia; si el CSS previo usa Inter, evita cargar ambas como fuente principal. Si cambiar la fuente implica una regresión importante, informa y solicita autorización antes de una sustitución masiva.
- Mantén `--mof-*` y las clases institucionales existentes por compatibilidad; no impongas la palabra MOF en títulos, rutas ni nombres propios de otros sistemas.

# Archivos de referencia: integrar, no sobrescribir indiscriminadamente
- Comprueba primero la estructura real, `package.json`, lockfile, `main.js`, configuración de Vuetify, estilos, gráficos e `index.html`; las rutas del ejemplo no son obligatorias.
- Para `designSystem.js`, compara la versión previa con la más reciente y conserva exports consumidos por la aplicación; incorpora los tokens nuevos sin eliminar APIs usadas.
- Para `themes.js`, adapta los temas claros/oscuros autorizados a la paleta oficial y conserva los demás temas existentes compatibles; no añadas cinco temas si el proyecto no los tiene.
- Para `style.css`, integra o fusiona estilos institucionales con el CSS actual sin reemplazar reglas específicas críticas ni duplicar imports.
- Para `vuetify.js`, reutiliza la instancia existente de `createVuetify`, plugins, localización y defaults; no dupliques el registro ni añadas componentes de labs si no se requieren.
- Para `highcharts.js`, integra configuración solamente si el proyecto ya usa Highcharts; para otra librería, transpón colores semánticos y estilos sin instalar Highcharts.
- Para `index.html`, conserva el punto de entrada real, metadatos, título, favicon y elemento raíz; modifica solo lo imprescindible para recursos ya disponibles y autorizados.
- Si los archivos maestros faltan en el proyecto, incorpóralos a la estructura real cuando los archivos oficiales estén disponibles y la tarea autorice la integración; informa si no están disponibles y no inventes su contenido.
- Consulta y actualiza la documentación obligatoria según la regla 00; reutiliza lo ya verificado durante la tarea.

# Compatibilidad de librerías y versiones
- Reutiliza Vue, Vuetify, Vite, el paquete de iconos y las herramientas de gráficos existentes; adapta la integración a las APIs instaladas y no presupongas Vuetify 4.
- No ejecutes instalaciones, migraciones ni cambios de lockfiles como parte de una mejora visual; usa Vue, Vuetify y CSS existentes y comunica alternativas compatibles.
- Valida los nombres de tema guardados en almacenamiento del navegador contra el conjunto permitido y aplica un tema por defecto seguro.
- No presupongas que `THEME_COLORS` cambia al alternar temas; configura gráficos y componentes a partir del tema activo.
- Usa la secuencia `SERIES_COLORS` para gráficos aplicables y actualiza texto, ejes y tooltips según el tema.

# Accesibilidad y comprobación
- Verifica contraste WCAG AA: al menos 4.5:1 para texto normal, 3:1 para texto grande y los componentes relevantes; no asumas cumplimiento por comentarios en CSS.
- Comprueba especialmente coral/blanco, verde/blanco y combinaciones de fondo/texto en modo oscuro; propone variantes accesibles sin cambiar arbitrariamente la paleta aprobada.
- Asegura foco visible, navegación por teclado y estados con significado textual además del color; revisa los temas existentes afectados, sin instalar recursos ni agregar modos nuevos.
- Verifica el resultado según las reglas 30 y 80, con los comandos y herramientas existentes; indica cualquier comprobación pendiente.

# Gestión de cambios y entrega
- Antes de aplicar cambios de integración que afecten 3 o más archivos, presenta lotes de 3 a 4 archivos al programador y espera confirmación según la regla 30. El carácter pequeño o seguro de un token o clase no permite omitir esa revisión.
- Antes de una migración de versión, sustitución masiva de estilos, actualización de paquetes o cambio de arquitectura, presenta un plan con archivos afectados, riesgos y pruebas y espera autorización.
- Al terminar, indica: archivos revisados y modificados, tokens/temas integrados, incompatibilidades solucionadas, pruebas ejecutadas y pendientes.
- No declares la integración terminada por copiar archivos sin verificar que estén cargados y utilizados en la interfaz.
