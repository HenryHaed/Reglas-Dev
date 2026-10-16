---
trigger: always_on
description: "Cómo modificar código sin reescribirlo y cómo reportar los cambios"
---

# Alcance y autonomía
- Localiza primero los componentes y estilos afectados; realiza cambios mínimos y coherentes con la tarea.
- No reformatees ni reescribas archivos completos sin necesidad, ni alteres pantallas, datos o comportamiento ajenos al alcance.
- Aplica directamente ajustes pequeños y reversibles ya autorizados: espaciado, alineación, clases, textos, estados y subcomponentes necesarios.
- No pidas confirmación por cada token compatible, archivo auxiliar o por superar 3-4 archivos. La cantidad de archivos no determina por sí sola el riesgo.
- Respeta el trabajo previo del usuario. No descartes cambios existentes ni realices renombrados, movimientos o eliminaciones ajenos a la tarea.

# Autorización según impacto
- Presenta una propuesta concreta y pide autorización si no existe ya para cambios incompatibles en contratos compartidos, arquitectura, identidad visual global, migraciones, dependencias, operaciones destructivas, despliegues o cambios de seguridad sensibles.
- Una instrucción explícita que ya autoriza el cambio no requiere una segunda confirmación del mismo alcance. Si aparece un impacto distinto, explica esa diferencia antes de actuar.
- Ante una ambigüedad que afecte comportamiento, permisos o alcance, consulta; para detalles visuales pequeños sigue el sistema existente y comunica la decisión.
- Un ajuste de CSS en un formulario de acceso no autoriza cambiar autenticación. Conserva los controles y aplica la regla 40 cuando cambie su funcionamiento.
- Reutilización y división de componentes: reglas 05 y 10. Si la extracción obliga a romper contratos, trata esa decisión como cambio de impacto.

# Verificación proporcional
- Antes de ejecutar comandos revisa los scripts y el gestor reales; no presupongas `npm run build` ni instales herramientas para verificar.
- Tras cambios de código, ejecuta la compilación y lint existentes cuando estén disponibles y sea posible. Ejecuta las pruebas relevantes al comportamiento modificado según la regla 80.
- Agrupa ediciones coherentes y verifica el resultado completo; repite controles si hay cambios posteriores relevantes, fallos o dudas pendientes, no tras cada ajuste de CSS.
- Para cambios exclusivamente documentales, verifica contenido, referencias y coherencia sin intentar compilar una aplicación inexistente.
- No crees tests que solo reproduzcan clases CSS o detalles internos para ajustes cosméticos de bajo impacto.
- Realiza revisión visual y de interacción en el área afectada con las herramientas disponibles; distingue lo observado de lo pendiente.
- No inventes resultados ni declares que una compilación demuestra accesibilidad o corrección visual.

# Entrega breve
1. Qué cambió y por qué.
2. Qué se reutilizó o creó y si afectó la documentación obligatoria.
3. Qué verificaciones se ejecutaron, sus resultados y limitaciones.
4. Riesgos o mejoras pendientes fuera del alcance, sin repetir toda la implementación.
