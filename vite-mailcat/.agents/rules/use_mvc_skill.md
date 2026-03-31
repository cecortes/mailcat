---
trigger: always_on
description: Ensure the AI always uses the apply_mvc_pattern skill when creating or modifying frontend components.
---

# Uso Obligatorio de la Skill "Apply MVC Pattern"

Esta regla es de cumplimiento **estricto y obligatorio** para cualquier asistente o IA que trabaje en este proyecto.

## Condición de Activación

Cualquier solicitud del usuario que implique interactuar, crear, modificar o refactorizar un componente frontend (por ejemplo, `LoginForm`, `UserTable`, `Modal`, vistas enteras o utilidades visuales) dentro del proyecto.

## Reglas a Seguir

1. **Delegación de Responsabilidad:** Antes de intentar escribir código para un componente frontend de forma independiente, debes **siempre** consultar y seguir la skill definida en el archivo `.agents/skills/apply_mvc_pattern/SKILL.md`.
2. **Aplicación Estricta:** Las instrucciones de la skill referenciada (arquitectura estricta de 4 archivos Modelo-Vista-Controlador-Factory, inyección de dependencias estricta sin imports internos, uso de clases ES6 y ESM) toman precedencia absoluta frente a las preferencias o conocimiento general de la IA para creación de componentes y frameworks.
3. **No Excepciones:** Bajo ninguna circunstancia se debe construir un componente front-end en un único archivo "spaghetti" ni violar el flujo unidireccional detallado en el factory pattern del componente en esta arquitectura. Todo componente nuevo o editado DEBE ajustarse al estándar MVC de la skill.
