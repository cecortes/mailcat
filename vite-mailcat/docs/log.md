# Code Log

Este archivo contiene el registro (log) de desarrollo del proyecto. Su objetivo es mantener un historial cronológico y estructurado de las decisiones técnicas, implementaciones, corrección de errores y características añadidas a lo largo del tiempo.

## Formato de cada entrada

Para mantener la consistencia y facilitar la lectura, cada nueva entrada en este documento debe seguir estrictamente este formato:

1. **Encabezado (H2):** Debe comenzar con la fecha en formato `DD-MM-YY` seguida de un guion y una descripción general de los cambios del día. (Ejemplo: `## 12-02-26 - Starting the code log`).
2. **Tareas Principales:** Usar una lista de viñetas (`- `) para describir las tareas mayores hechas durante ese día de manera resumida.
3. **Subtareas / Checklist:** Utilizar listas anidadas con casillas de verificación de Markdown para detallar los pasos y su estado:
   - `- [x]` para tareas completadas.
   - `- [ ]` para tareas pendientes.
   - `- [-]` para tareas en las que se empezó a trabajar pero aún no concluyen.
4. **Separación:** Al finalizar todas las tareas de una entrada, se debe añadir un separador de línea (`---`) como cierre antes de la siguiente fecha.

### Ejemplo visual:

```markdown
## 12-02-26 - Starting the code log

- Started the project in vite, the goal is create simple components such as login form, dashboard, etc. Components that we can re use in the future.

- Install tailwindcss and @tailwindcss/vite via npm.
  - [x] Create the vite project.
  - [x] Install tailwindcss and @tailwindcss/vite via npm.

---
```

---

## 24-03-26 - Initial project setup

- [x] Initial project setup
- [x] Cleaned up unnecessary files
- [x] Set up basic project structure
- [x] Generate SRS document
  - [x] Create the Software Requirements Specification (SRS.md) document for MailCat.
    - [x] Document the project summary and core goals.
    - [x] Define the project architecture (Vite, JS, MVC) and independent components.
    - [x] Document the AI core features powered by Gemini 3 Flash.
    - [x] Establish backend and data management guidelines for the MVP.
    - [x] Outline the styling guide reference.

---
