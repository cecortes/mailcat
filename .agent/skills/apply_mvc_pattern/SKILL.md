---
name: apply_mvc_pattern
description: Genera o refactoriza un componente frontend aplicando estrictamente el patrón MVC con Inyección de Dependencias vía Factory y módulos ESM para Vite.
---

# Patrón MVC en Componentes Frontend (Vite/ESM)

Cuando el usuario te solicite crear, aplicar o refactorizar un componente (por ejemplo, `LoginForm`, `UserTable`, `Modal`, etc.) **DEBES** seguir estrictamente las siguientes reglas:

## 1. Estructura de Archivos

DEBES separar el código del componente en exactamente 4 archivos dentro de una carpeta dedicada al componente. No debes mezclar responsabilidades en un solo archivo.

- `{Componente}Model.js`
- `{Componente}View.js`
- `{Componente}Controller.js`
- `{Componente}Factory.js` (o un `index.js` que actúe como Factory)

## 2. Reglas Comunes Obligatorias (MANDATORY)

- **Clases ES6:** DEBES utilizar la sintaxis de `class` para permitir múltiples instancias del componente.
- **Exports Nombrados:** NO uses `export default`. DEBES utilizar `export` nombrado (ej. `export class UserModel`) para facilitar el tree-shaking.
- **Prohibido Importar Dependencias Internas:** El Controlador, el Modelo y la Vista **NO DEBEN** importar otros módulos de la app o instancias de su triada MVC directamente. Toda dependencia que necesiten (servicios, el modelo o la vista) DEBE ser inyectada a través de sus respectivos constructores.

## 3. El Modelo (Model)

**Responsabilidad:** Gestionar el estado local del componente y la lógica de negocio.

- NO DEBE tener referencias al DOM, ni a `document`, ni a la Vista.
- Recibe cualquier dependencia estricta (ej. servicios de red, APIs, stores globales) a través de su constructor.
- Los métodos que impliquen comunicación de red REST/APIs deben ser asíncronos (`async/await`).

## 4. La Vista (View)

**Responsabilidad:** Construir el HTML, insertarlo en el DOM y capturar eventos nativos.

- En el `constructor`, recibe un elemento raíz (`this.root = rootElement`) y cualquier otra dependencia visual si fuera el caso.
- NO DEBE contener lógica de negocio, validaciones complejas o llamadas a APIs.
- Las referencias a elementos del DOM en las propiedades de la clase **deben usar el prefijo `$`** (ej. `this.$form = this.root.querySelector('#user-form')`).
- Debe exponer métodos `bind{Evento}(handler)` para que el Controlador inyecte la lógica.

## 5. El Controlador (Controller)

**Responsabilidad:** Coordinar la comunicación y ser el puente entre el Modelo y la Vista.

- En su `constructor`, recibe las instancias ya creadas e inyectadas del Modelo y de la Vista (ej. `constructor(model, view)`).
- Define los métodos `handle{Accion}` y los inyecta en la Vista utilizando los métodos `bind{Evento}` de la misma.
- Responde a los eventos del usuario delegando estados/datos al modelo y actualizando la vista según sea necesario.

## 6. El Factory (Factory o Index)

**Responsabilidad:** Ensamblar e inyectar las dependencias del componente.

- Es el **ÚNICO** archivo del componente que tiene permitido importar a `Model.js`, `View.js`, `Controller.js` y las dependencias externas (servicios, clientes de API de Vite, utilities).
- Instancia el Modelo (inyectándole servicios).
- Instancia la Vista (inyectándole nodos DOM u otros).
- Instancia el Controlador (pasándole el Modelo y la Vista recién creados).
- Retorna el Controlador instanciado para que el resto de la aplicación lo inicie.

## 7. Flujo de Datos (Data Flow)

Sigue estas fases al aplicar cambios:

1. **Ensamblaje:** El punto de entrada o componente padre invoca a `{Componente}Factory.create(rootNode)` que devuelve el controlador ensamblado.
2. **Render:** Se llama a la inicialización, usualmente una función dentro de controlador o vista, que arranca la interfaz y muestra los datos.
3. **Interacción:** El usuario interactúa. La Vista captura el evento nativo y ejecuta el callback `handler` inyectado por el Controlador.
4. **Proceso:** El Controlador intercepta el evento (en un método `handle...`) y lee/escribe los datos mutando el Modelo a través de sus métodos.
5. **Actualización:** El Controlador evalúa la respuesta del Modelo y envía la instrucción a la Vista para que renderice o modifique el DOM.
