---
trigger: always_on
description: Ensure the AI always uses the write_code_log skill when creating or modifying code log entries.
---

# Uso Obligatorio de la Skill "Write Code Log"

Esta regla es de cumplimiento **estricto y obligatorio** para cualquier asistente o IA que trabaje en este proyecto.

## Condición de Activación

Cualquier solicitud del usuario que implique interactuar, crear, modificar o añadir una entrada en el archivo de registro de cambios del proyecto (`vite-mailcat/docs/log.md`), ya sea de forma explícita ("agrega al log", "crea la entrada diaria") o de forma implícita (como parte del flujo de finalización de una tarea).

## Reglas a Seguir

1. **Delegación de Responsabilidad:** Antes de intentar escribir en el archivo de forma manual y sin contexto, debes **siempre** instanciar o usar la herramienta de visualización (`view_file`) para consultar y seguir la skill definida en el archivo `.agents/skills/write_code_log/SKILL.md`.
2. **Aplicación Estricta:** Las instrucciones de la skill referenciada (formato Markdown, reglas de idioma en inglés, y ubicación al final del documento principal protegido) toman precedencia absoluta frente a cualquier conocimiento general de la IA.
3. **No Excepciones:** Bajo ninguna circunstancia se debe actualizar el archivo de registro general `vite-mailcat/docs/log.md` sin seguir línea por línea las validaciones impuestas por la skill.
