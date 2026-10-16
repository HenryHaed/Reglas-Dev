---
trigger: glob
description: "Convenciones Vue 3 y Vuetify de acuerdo con las versiones reales instaladas, en JavaScript"
globs: "**/*.vue"
---

# Compatibilidad
- Verifica Vue y Vuetify reales según la regla 00; no presupongas Vuetify 3 ni Vuetify 4.
- Usa APIs soportadas y patrones verificados. Consulta documentación ante dudas; no repitas consultas por cada uso de una prop ya comprobada.
- No añadas componentes experimentales o de labs para resolver un diseño habitual. Usa alternativas estables disponibles.
- Evita APIs deprecadas en código nuevo cuando exista una alternativa compatible; no migres código ajeno a la tarea.

# Componentes Vue
- En Vue 3 usa JavaScript y `<script setup>`. No migres componentes existentes solo para cambiar su estilo.
- Declara props con tipo, obligatoriedad y valores por defecto; para arrays/objetos usa una función de fábrica.
- Declara emits y documenta los contratos relevantes. Usa `defineModel()`, `useTemplateRef` u otras APIs solo si la versión instalada las soporta.
- Usa `computed` para valores derivados y `watch` para efectos secundarios; evita watchers profundos o repetidos sin necesidad.
- Usa claves únicas y estables en listas. No combines `v-if` y `v-for` en el mismo elemento.
- Libera listeners, timers, suscripciones y URLs de objeto al terminar su uso o desmontar el componente.

# Tamaño y mantenimiento: 150 a 300 líneas
- El rango de revisión es de 150 a 300 líneas; 150 no es un mínimo ni un punto de división automática. Un componente puede tener menos líneas si mejora su claridad y mantenimiento.
- El máximo es 300 líneas por archivo `.vue` nuevo o reorganizado dentro del alcance. Cuenta todas las líneas físicas: template, script, estilos, comentarios y líneas en blanco.
- Entre 150 y 300 líneas evalúa responsabilidades, complejidad, contratos y facilidad de prueba. Divide antes si mezcla tareas o se vuelve difícil de mantener.
- Antes de superar 300 líneas, extrae responsabilidades coherentes a subcomponentes, composables o estilos compartidos cuando corresponda. No comprimas código ni traslades bloques arbitrarios para eludir el límite.
- Si un componente heredado ya supera 300 líneas, identifica el problema al intervenirlo y aplica una extracción localizada cuando esté dentro del alcance. Si requiere una refactorización amplia no autorizada, informa el conflicto y el trabajo pendiente; no declares que cumple el límite ni reorganices todo el módulo.
- Mantén contratos retrocompatibles y revisa los usos afectados tras una extracción. No fragmentes elementos triviales únicamente para alcanzar un número.

# Organización y rendimiento
- Reutiliza las capas reales según la regla 05: estado local para uso local, store para estado compartido y clientes HTTP existentes para acceso a datos.
- Evita peticiones duplicadas y cálculos costosos repetidos durante el renderizado.
- En búsquedas remotas, reutiliza la espera existente o un temporizador nativo cuando sea necesario; cancela peticiones anteriores si el cliente lo soporta o ignora respuestas obsoletas.
- Para listas grandes, usa paginación. Considera virtualización solo si ya está disponible en la versión instalada y preserva accesibilidad y funcionamiento.
- Conserva la carga diferida de rutas existente y carga componentes pesados cuando se necesiten; no conviertas cada componente pequeño en asíncrono.
- Mide con herramientas disponibles antes de introducir optimizaciones complejas; no afirmes mejoras de rendimiento sin medición.

# Vuetify, responsive y CSS
- Prioriza componentes, props, slots y utilidades disponibles en Vuetify; reutiliza los componentes propios que aporten valor.
- Usa el tema y tokens existentes con APIs compatibles. No impongas `useTheme` o `useDisplay` si la versión no los ofrece.
- Para distribución visual usa CSS nativo, media queries y utilidades disponibles. Usa lógica de breakpoint solo cuando cambie el comportamiento, evitando listeners de resize innecesarios.
- Personaliza CSS siguiendo la regla 90; no cambies registros de plugins ni el orden global de estilos por un ajuste local.
- Usa únicamente iconos, fuentes y recursos existentes; no instales paquetes.
- Reutiliza validadores reales y `v-form` cuando corresponda, sin inventar `src/utils/validators.js`.

# Calidad
- Aplica la UX/UI de la regla 85 y las verificaciones de la regla 80.
- Respeta lint y convenciones existentes; no desactives reglas para hacer pasar el código.
- Actualiza el catálogo cuando cambien componentes reutilizables o sus contratos; no por cambios cosméticos sin impacto en el catálogo.
