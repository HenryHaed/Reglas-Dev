---
trigger: always_on
description: "Respetar el código, la estructura y las decisiones ya existentes"
---

# Reutilizar con criterio
- Antes de crear componentes, consulta el catálogo según la regla 00 y busca implementaciones reales en el área afectada.
- Reutiliza o extiende de forma retrocompatible cuando exista la misma responsabilidad y un contrato adecuado. Conserva props, emits, slots y comportamiento de los consumidores.
- La segunda repetición invita a revisar, no obliga a extraer. Separa una abstracción cuando reduzca mantenimiento y tenga un propósito estable.
- Evita componentes genéricos con muchas banderas, excepciones por pantalla o dependencias de negocio ajenas. Tampoco crees envoltorios de Vuetify que no aporten comportamiento o consistencia.
- Sigue las convenciones predominantes del módulo y la configuración del proyecto; no elijas una variante solo por ser la más reciente.

# Estructura y estado
- Localiza vistas, layouts, clientes HTTP, stores, utilidades, composables y CSS existentes; no impongas carpetas ni nombres de otro proyecto.
- Mantén el estado de una sola vista o componente en su ámbito local. Usa un store existente para estado realmente compartido o cuando lo exija la arquitectura verificada.
- Reutiliza los clientes HTTP y mecanismos de sesión y errores; no obligues a pasar por un store nuevo para cada petición.
- Separa lógica de negocio y presentación cuando mejore mantenimiento; usa las capas existentes sin crear arquitecturas paralelas.
- Respeta URLs, nombres de rutas y estilos globales ya consumidos. Evita renombrados y hojas globales duplicadas.

# Cambios dentro del alcance
- Aplica los criterios de tamaño de la regla 10 al componente intervenido, sin reorganizar módulos ajenos.
- Los subcomponentes y archivos locales necesarios siguen la estructura existente y cuentan en el umbral de la regla 30: desde 3 archivos, presenta el lote al programador y espera confirmación antes de aplicarlo; no los crees por decisión unilateral para evitar la consulta.
- Conserva contratos e imports, incluidos los dinámicos, y las mayúsculas/minúsculas correctas. No elimines ni muevas archivos ajenos a la tarea.
- Refactorizaciones amplias, cambios de contratos compartidos o de arquitectura siguen la regla 30.
- Reporta mejoras fuera del alcance sin aplicarlas.
