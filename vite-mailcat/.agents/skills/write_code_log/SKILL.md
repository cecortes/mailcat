---
name: write_code_log
description: Escribe una nueva entrada estructurada en el archivo de registro del proyecto (docs/log.md) siguiendo estrictamente el formato del equipo.
---

# Write Code Log

Esta skill define las instrucciones exactas para registrar los avances, decisiones técnicas y tareas realizadas en el archivo `vite-mailcat/docs/log.md`. El objetivo es mantener el historial cronológico estructurado, coherente y fácil de leer.

## 1. Contexto y Reglas Generales

1. **Ubicación del Archivo:** Las entradas SIEMPRE deben agregarse al archivo `d:\GITHUB\mailcat\vite-mailcat\docs\log.md`.
2. **Posición de la Nueva Entrada:** La nueva entrada debe añadirse **al final** del documento, justo después del último separador `---`.
3. **Idioma:** Escribe la entrada **estrictamente en inglés**, independientemente del idioma en el que el usuario te dé las instrucciones.

## 2. Formato Estricto y Ejemplos

Toda nueva entrada DEBE cumplir exactamente con esta estructura Markdown:

```markdown
## DD-MM-YY - Título descriptivo general

- Tarea principal 1 (resumen de lo logrado)
  - [x] Subtarea o detalle técnico completado
  - [ ] Subtarea o paso pendiente
  - [-] Subtarea en progreso o pausada

- Tarea principal 2
  - [x] Detalle de la tarea 2

---
```

### Explicación de las partes:

- **Encabezado (H2):** Inicia con la fecha en formato día-mes-año (`DD-MM-YY`), seguido de un guion y un título conciso. Ejemplo: `## 24-03-26 - Creando nuevo componente de login`. (La fecha debe ser estrictamente la fecha actual).
- **Tareas Principales:** Usa la viñeta de guion (`- `) para listar las actividades a gran escala.
- **Subtareas (Checklist):** Usa un nivel de indentación (dos espacios) debajo de la tarea principal. Utiliza los corchetes para indicar estado:
  - `- [x]`: Tarea completada.
  - `- [ ]`: Pendiente / Planeado.
  - `- [-]`: En curso / Iniciada pero no concluida.
- **Línea Separadora:** Al final de TODA la entrada, de forma obligatoria, añade un separador `---` rodeado de líneas en blanco, tal como se ve en el ejemplo.

## 3. Instrucciones de Ejecución (Para la IA)

Cuando un usuario te pida "agregar al log", "escribir en el log", o invoque esta skill:

1. **Analiza el contexto:** Lee la solicitud del usuario o resume los cambios realizados recientemente en tu historial de conversación para deducir qué tareas y subtareas se han llevado a cabo.
2. **Prepara el bloque de texto:** Redacta el bloque Markdown asegurándote de usar la fecha correcta (`DD-MM-YY`) y cumplir al 100% con la estructura de listas y checkboxes mencionada.
3. **Modifica el archivo:**
   - Lee el archivo `d:\GITHUB\mailcat\vite-mailcat\docs\log.md` usando la herramienta `view_file`.
   - Modifícalo usando `replace_file_content` o `multi_replace_file_content` para insertar tu nuevo bloque **al final** del archivo, cuidando de no alterar las entradas anteriores.
4. **Verifica:** Asegúrate de que tu bloque insertado términa fielmente con una nueva línea y un `---`.
