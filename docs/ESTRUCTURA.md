# Estructura del paquete de reglas frontend

## Alcance verificado

Esta carpeta contiene instrucciones para agentes de desarrollo frontend. No contiene una aplicación Vue, `package.json`, lockfiles, componentes `.vue`, router, stores ni configuración ejecutable de Vuetify. No hay repositorio Git en esta carpeta.

## Archivos y directorios

| Ruta | Función |
| --- | --- |
| `AGENTS.md` | Punto de entrada para Codex/OpenCode y referencia a las reglas detalladas. |
| `README.md` | Instalación y uso del paquete en un proyecto receptor. |
| `.cursor/rules/*.mdc` | Reglas detalladas con metadatos de activación de Cursor. |
| `.agents/rules/*.md` | Reglas equivalentes con metadatos de activación de Antigravity. |
| `docs/ESTRUCTURA.md` | Inventario verificable de este paquete. |
| `docs/COMPONENTS.md` | Estado del catálogo de componentes de este paquete. |
| `docs/MEJORAS-FRONTEND.md` | Registro autorizado de cambios y verificaciones de las reglas. |

## Reglas disponibles

Hay 14 pares de reglas. Las reglas 00 y 30 definen el flujo de trabajo; 05 trata reutilización; 10 define componentes, tamaño y rendimiento; 20, 40, 50, 60 y 70 cubren seguridad, evidencias, privacidad y errores; 80 trata verificación; 85 define UX/UI; 90 define identidad y CSS; 100 trata compatibilidad y 110 integración de recursos maestros.

El límite de componentes se aplica a los archivos `.vue` del proyecto receptor: revisión entre 150 y 300 líneas, máximo de 300 en componentes nuevos o reorganizados, y componentes menores cuando beneficie el mantenimiento. No hay archivos `.vue` en este paquete a los que aplicar el conteo.

## Mantenimiento

Los pares de reglas de Cursor y Antigravity deben conservar el mismo cuerpo; sus encabezados dependen de la herramienta. Las referencias a Vue, Vuetify, clientes HTTP, estilos y tokens describen recursos que deben comprobarse en el proyecto receptor, no archivos incluidos en este paquete.

Cuando se adopten estas reglas en una aplicación, sus documentos de estructura y componentes deben describir esa aplicación. No se debe sobrescribir documentación válida con los inventarios de este paquete.
