---
trigger: glob
description: "Uso obligatorio de tokens institucionales y estilos en frontend, según librerías y versiones reales"
globs: "src/**/*.vue,src/**/*.js,src/**/*.css,index.html"
---

# Identidad y alcance
- MOF identifica el origen del estándar, no el nombre obligatorio del proyecto. Conserva los identificadores oficiales de tokens y clases.
- Aplica la identidad institucional al componente, sección o flujo nuevo o modificado dentro de la tarea. Un cambio local no obliga a rediseñar toda la pantalla ni las vistas restantes.
- Reutiliza archivos maestros y ubicaciones reales; no asumas carpetas, librerías o versiones. Si faltan los recursos oficiales, solicítalos y continúa solo lo que no dependa de ellos.
- La obligación es obtener un resultado visual y funcional coherente, no copiar archivos completos ni migrar dependencias.
- Usa la jerarquía de recursos de la regla 110 para integrar referencias. Las decisiones de identidad global requieren autorización; los ajustes locales compatibles siguen la regla 30.

# Semántica institucional
- Usa petróleo para navegación y acciones estándar, turquesa para interacción y herramientas, coral para guardar/crear y rojo para eliminar, según los tokens oficiales.
- Reutiliza `btn-cta`, `btn-primary`, `btn-secondary`, `btn-neutral` y `btn-danger`, o equivalentes existentes con la misma semántica.
- Mantén una acción dominante por tarea; no conviertas todas las acciones en CTA ni uses el estilo CTA para acciones destructivas.
- Usa las clases de estado existentes (`chip-activo`, `chip-pendiente`, `chip-rechazado`, `chip-borrador`, `chip-categoria`, `badge-contador`) solo cuando comuniquen información útil.
- En tablas, reutiliza acciones e iconos existentes con etiquetas accesibles y permisos conservados.
- Aplica las pautas de contenido, formularios, tablas y carga informativa de la regla 85.

# Orden de personalización de Vuetify
1. Props, slots y utilidades públicas compatibles con la versión instalada.
2. Tema, tokens y defaults ya existentes, cuidando el alcance de cualquier cambio compartido.
3. Clases maestras compartidas cuando el patrón sea común.
4. CSS local con `<style scoped>` para ajustes particulares.
5. `:deep()` solo para un ajuste interno concreto que no pueda resolverse de forma suficiente con las opciones anteriores; acótalo bajo una clase propia del componente.

# CSS mantenible
- Usa CSS nativo; no instales Sass, Tailwind, librerías de animación, iconos, fuentes ni herramientas adicionales.
- Reutiliza variables `--mof-*` y tokens oficiales disponibles para color, separación, tipografía, radios y elevación. No inventes nombres de tokens ni valores institucionales ausentes.
- Mantén clases con propósito claro y selectores cortos. Evita cadenas dependientes de la estructura interna de Vuetify, selectores por posición y sobrescrituras globales para un único caso.
- No acumules `!important`; si una excepción es inevitable, acótala y justifica su necesidad. Revisa especificidad, orden de carga y CSS layers solo si el proyecto los utiliza.
- No dupliques estilos maestros ni imports. Promueve una regla local a compartida cuando haya un patrón estable y consumidores identificados.
- Para añadir clases locales o variantes compatibles, respeta el umbral de la regla 30: desde 3 archivos, presenta los cambios al programador y espera confirmación. No alteres tokens compartidos ni defaults con impacto global no autorizado.
- No reestructures el tema ni cambies el registro de Vuetify para corregir un detalle visual.
- Al personalizar menús o diálogos, comprueba dónde se renderiza su contenido y usa el mecanismo público compatible para acotar sus estilos; no amplíes CSS global sin necesidad.

# Distribución y claridad visual
- Reutiliza la escala de espaciado y jerarquía tipográfica existentes; alinea títulos, campos, tablas y acciones.
- Prefiere grid/flex, anchos adaptables y espacio suficiente. Evita alturas fijas que recorten texto, errores o contenido traducido.
- Diseña responsive con media queries o utilidades existentes; conserva acceso a información y acciones esenciales en móvil y con zoom.
- Usa bordes, sombras y fondos para agrupar, sin decorar cada dato. Evita degradados, desenfoques y animaciones que no aporten comprensión.
- Mantén estados normal, hover, foco, selección, error y deshabilitado distinguibles. No elimines indicadores de foco.
- Las transiciones deben ser discretas, evitar trabajo visual innecesario y respetar `prefers-reduced-motion`.

# Temas, fuentes y gráficos
- Usa los temas existentes; revisa texto, superficies, bordes, foco y estados en claro/oscuro y en otros temas disponibles afectados.
- No supongas que un objeto de colores cambia automáticamente con el tema activo.
- Conserva la tipografía oficial ya cargada; no añadas fuentes externas para un ajuste visual. La integración de recursos oficiales sigue la regla 110.
- Usa `SERIES_COLORS` en gráficos existentes cuando esté disponible y adapta texto, ejes y tooltips al tema real; no instales motores de gráficos.

# Accesibilidad y comprobación
- Verifica contraste real: al menos 4.5:1 en texto normal, 3:1 en texto grande y 3:1 en componentes relevantes. No declares conformidad solo por usar tokens oficiales.
- Si una combinación falla, reutiliza una variante accesible aprobada cuando exista; para cambiar identidad o tokens globales informa el conflicto y solicita la decisión pendiente.
- No dependas solo del color: conserva texto, iconos con nombre accesible y estados comprensibles.
- Revisa los componentes y temas afectados con la regla 80; aplica las verificaciones de compilación y reporte de la regla 30.
- Indica lo que no pudiste observar o medir. Estas reglas no autorizan cambios de backend o infraestructura.
