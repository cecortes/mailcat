---
name: apply_mvc_pattern
description: Genera o refactoriza un componente frontend aplicando estrictamente el patrón MVC con Inyección de Dependencias vía Factory y módulos ESM para Vite.
---

# Patrón MVC en Componentes Frontend (Vite/ESM)

Cuando el usuario te soliciten crear, aplicar o refactorizar un componente (por ejemplo, `LoginForm`, `UserTable`, `Sidebar`, `Dashboard`, `InputUserArea`, `Modal`, `Validator`, etc.) **DEBES** seguir estrictamente las siguientes reglas basadas en la directriz de arquitectura oficial del proyecto.

## 1. Estructura de Archivos y Ubicación

En este proyecto **TODO es un componente** y se aloja en `src/components/`. No existen carpetas como `services` ni `utils`.
DEBES separar el código del componente en exactamente 4 archivos dentro de una carpeta dedicada al componente. No debes mezclar responsabilidades en un solo archivo.

- `{Componente}Model.js`
- `{Componente}View.js`
- `{Componente}Controller.js`
- `{Componente}Factory.js` (o un `index.js` que actúe como Factory)

## 2. Reglas Comunes Obligatorias (MANDATORY)

- **Clases ES6:** DEBES utilizar la sintaxis de `class` para permitir múltiples instancias del componente.
- **Exports Nombrados:** NO uses `export default`. DEBES utilizar `export` nombrado (ej. `export class UserModel`) para facilitar el tree-shaking.
- **Prohibido Importar Dependencias Internas:** El Controlador, el Modelo y la Vista **NO DEBEN** importar partes de su propia triada directamente. Toda dependencia que necesiten DEBE ser inyectada a través de sus respectivos constructores.

## 3. El Modelo (Model)

**Responsabilidad:** Gestionar el estado local del componente, lógica de negocio y comunicaciones HTTP/APIs.

- NO DEBE tener referencias al DOM, ni a `document`, ni a la Vista.
- **Lógica Externa/APIs:** Dado que no existen servicios globales centralizados, toda conexión (ej. llamadas a la API de Gemini, Fetch general al backend) debe implementarse **directamente dentro de los métodos del Modelo**. 
- **Persistencia Restringida:** Toda persistencia de datos debe hacerse única y estrictamente a través de **LocalStorage**.
- Los métodos que impliquen comunicación de red REST/APIs deben ser asíncronos (`async/await`).

## 4. La Vista (View)

**Responsabilidad:** Construir el HTML, insertarlo en el DOM y capturar eventos nativos.

- En el `constructor`, recibe un elemento raíz (`this.root = rootElement`) y cualquier otra dependencia visual si fuera el caso.
- NO DEBE contener lógica de negocio, validaciones transaccionales o llamadas a APIs.
- Las referencias a elementos explícitos del DOM en las propiedades de la clase **deben usar el prefijo `$`** (ej. `this.$form = this.root.querySelector('#user-form')`).
- Debe exponer métodos `bind{Evento}(handler)` para que el Controlador inyecte la lógica.

## 5. El Controlador (Controller)

**Responsabilidad:** Coordinar la comunicación y ser el pegamento exclusivo entre el Modelo y la Vista.

- En su `constructor`, recibe las instancias ya creadas e inyectadas del Modelo y de la Vista (ej. `constructor(model, view)`).
- Define los métodos que inyecta en la Vista utilizando los métodos `bind{Evento}` de la misma.
- Responde a los eventos interactivos del usuario delegando procesamiento/fetches al modelo, y con el retorno exitoso de estas promesas, ordena a la Vista su inmediata actualización declarativa.

## 6. El Factory (Factory o Index)

**Responsabilidad:** Ensamblar e inyectar independientemente las dependencias del componente.

- Es el **ÚNICO** archivo de la arquitectura MVC autorizado para importar a `Model.js`, `View.js`, `Controller.js` e instanciar clases de otros componentes (como un Validator).
- Instancia el Modelo.
- Instancia la Vista (inyectándole el fragmento del DOM, usualmente `this.root`).
- Instancia el Controlador (pasándole el Modelo y la Vista instanciados en los pasos anteriores).
- Retorna la instancia completa del Controlador para que un componente padre o router lo encienda.

## 7. Flujo de Datos (Data Flow)

Sigue estas fases al aplicar cambios o diseñar:

1. **Ensamblaje:** El router o componente padre invoca a `{Componente}Factory.create(rootNode)` que devuelve el controlador ensamblado.
2. **Inyección:** El Controlador usa métodos como `bindSubmit` para colgar y escuchar los eventos nativos de la vista delegando *handlers* anónimos.
3. **Interacción:** El usuario interactúa. La Vista captura el evento nativo del DOM y ejecuta el `handler` inyectado por el Controlador de manera "tonta".
4. **Proceso:** El Controlador lidera y ordena al Modelo proceder con mutaciones, llamados de API Gemini o guardados en LocalStorage a través de sus métodos.
5. **Re-render:** El Controlador recibe el éxito del Modelo y ordena a la Vista que dibuje la interfaz con la mutación efectuada.

## 8. Renderizado Obligatorio (DOMParser)

Para asegurar consistencia, modularidad y seguridad, **todas las vistas** deben usar obligatoriamente explícitamente `DOMParser` para todo el renderizado. Cualquier inyección de nuevos elementos visuales al DOM debe hacerse mediante la construcción dinámica de strings (Template Literals) convirtiéndolos a nodos HTML con esta API en lugar de métodos como `innerHTML` directo en el documento o creaciones imperativas sueltas con `document.createElement`.

## 9. Gestión de Estilos CSS

El proyecto se regirá por una hoja de estilos globalizada. Debe existir un archivo llamado `styles.css` ubicado en la raíz del proyecto, en el cual estarán definidos todos los estilos CSS para todo el proyecto y todos sus componentes. Queda proscrito el uso de módulos CSS disgregados o archivos de estilos por carpeta de componente.
