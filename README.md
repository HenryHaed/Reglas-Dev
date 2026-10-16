# Paquete frontend institucional — instalación

Extrae el ZIP en la raíz del proyecto frontend (junto a `package.json`, si existe). No sustituyas código ni archivos maestros existentes por las copias de referencia.

- **Cursor:** `.cursor/rules/*.mdc`.
- **Antigravity:** `.agents/rules/*.md`.
- **VS Code con Codex / OpenCode:** `AGENTS.md`, que remite a las reglas detalladas. No se requiere `.github/copilot-instructions.md` salvo que también se use GitHub Copilot.

`docs/ESTRUCTURA.md` y `docs/COMPONENTS.md` deben generarse desde el código real si faltan. Otros documentos nuevos requieren autorización.

Las versiones de Vue/Vuetify se detectan por proyecto; está prohibido migrar paquetes sin autorización. La identidad visual institucional sí es obligatoria en las pantallas del alcance solicitado.

**Importante:** las reglas dan instrucciones a asistentes, no instalan dependencias ni modifican automáticamente pantallas sin una tarea del desarrollador.

## Alcance de las mejoras
- Vue, Vuetify y CSS nativo ya disponibles, sin instalaciones ni migraciones para tareas visuales.
- UX/UI sencilla, contenido directo, estados comprensibles y personalización de CSS con alcance controlado.
- Componentes: revisión entre 150 y 300 líneas y máximo de 300 líneas físicas en archivos `.vue` nuevos o reorganizados; pueden ser menores por mantenimiento. Los heredados mayores se reportan y se tratan según el alcance, sin afirmar cumplimiento ficticio.
- Confirmación obligatoria del programador desde 3 archivos afectados, también para CSS, textos y documentación. Presenta archivos, cambios y pruebas antes de editar; para trabajos mayores, confirma cada lote de 3 a 4 archivos (el último puede ser menor). No dividas artificialmente el trabajo para evitar el umbral. La regla 30 detalla el conteo y las aprobaciones adicionales por impacto.

Las reglas 85 (UX/UI) y 90 (identidad/CSS) se complementan. Las reglas 00 y 30 concentran el flujo de trabajo; la 10 define tamaño, organización y rendimiento; la 80 define verificaciones.

En monorepositorios, ajusta los patrones de activación al módulo frontend real. Los patrones no sustituyen la comprobación del contexto: no apliques reglas Vue a código de backend.

## Documentación del paquete
- [Estructura](docs/ESTRUCTURA.md)
- [Catálogo de componentes](docs/COMPONENTS.md)
- [Mejoras implementadas y verificaciones](docs/MEJORAS-FRONTEND.md)

Estos documentos describen este paquete de instrucciones, no una aplicación Vue. Al instalarlo, conserva la documentación válida del proyecto receptor y actualízala desde su código; no la sustituyas por el inventario del paquete. Los archivos maestros institucionales deben obtenerse del proyecto o de los recursos oficiales proporcionados.
