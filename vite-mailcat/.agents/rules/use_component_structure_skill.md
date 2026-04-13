---
trigger: always_on
description: Ensure the AI always uses the create_component_structure skill to set up the correct directory structure before doing anything else for a new component.
---

# Uso Obligatorio de la Skill "Create Component Structure"

Esta regla es de cumplimiento **estricto y obligatorio** para inicializar la estructuración de todo nuevo componente frontend dentro del proyecto.

## Reglas a Seguir

1. **Precedencia Absoluta:** Esta regla y la skill asociada (`.agents/skills/create_component_structure/SKILL.md`) tienen **prioridad y precedencia máxima** por sobre cualquier otra regla o skill destinada a la creación o estructuración de código de componentes.
2. **Paso Previo Obligatorio (Verificación y Creación):** Antes de crear cualquier archivo de código (JS/CSS) o añadirle contenido a un nuevo componente, **DEBES de forma imperativa** ejecutar la skill `create_component_structure` primero.
3. **Flujo de Acción Estricto para Nuevos Componentes:**
   - **Paso 1:** Preguntar al usuario el nombre del componente (conforme a la skill `create_component_structure`) y esperar su respuesta.
   - **Paso 2:** Crear la estructura de carpetas (`Controller`, `Model`, `View`, `Icons`) con sus `.gitkeep` vacíos, asegurando que la estructura sea la correcta.
   - **Paso 3:** Solo entonces, cuando la estructura base de carpetas esté creada y confirmada correctamete, estarás autorizado a aplicar las otras lógicas de desarrollo o usar otras skills (como llenar esos directorios usando `apply_mvc_pattern`).
4. **Prohibición de atajos:** **NUNCA** debes escribir ni una sola línea de código, ni generar la lógica MVC para un nuevo componente, sin haber validado y garantizado primero la creación de las carpetas subyacentes exactas estipuladas.
