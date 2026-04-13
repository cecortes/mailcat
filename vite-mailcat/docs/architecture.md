# Arquitectura del Proyecto MailCat

Este documento fundamenta la arquitectura frontend estricta que todo nuestro código debe seguir. Su propósito es que tanto desarrolladores humanos como las IAs comprendan e implementen este patrón de manera consistente a lo largo de todo el proyecto.

## 1. Visión General: SPA con Vanilla JS

El frontend imita el comportamiento de una Single Page Application (SPA) y Frameworks robustos usando Vanilla JS:

Router Propio (src/components/router/router.js): Modifica el historial de navegación (History API) e intercepta el estado de recarga para inyectar componentes dinámicamente en el div #app sin recargar la página.
Estructura de Componentes MVC: Cada funcionalidad principal o "página" (como Login, Dashboard o Modales) se divide en tres partes:
View (*View.js): Se encarga exclusiva y declarativamente de renderizar el HTML (por medio de strings construidos dinámicamente y el DOMParser) y de retornar referencias a los elementos DOM (LoginElements).
Model (*Model.js): Gestiona los datos y se comunica con las APIs externas mediante fetch hacia el backend.
Controller (*Controller.js): Actúa de pegamento. Inyecta eventos (addEventListener) a la View y comunica las acciones al Model. También utiliza clases auxiliares, como validadores o gestores de almacenamiento (LocalStorage).

## 2. Implementación Estricta MVC: La Regla de 4 Archivos y Componentización Absoluta

Aunque los componentes se conceptualizan en 3 capas fundamentales en el resumen anterior, la implementación física en nuestro proyecto exige un **cuarto archivo clave: el Factory**.

En este proyecto **TODO es un componente**. No existen carpetas como `services` ni `utils`. Toda funcionalidad (sea el Validador, conectores a Gemini, o utilidades sueltas) reside en su respectiva carpeta dentro de `src/components/` y se rige, siempre que la lógica lo permita, bajo una estructura de cuatro archivos funcionales:

- `{Componente}Model.js`
- `{Componente}View.js`
- `{Componente}Controller.js`
- `{Componente}Factory.js` (o `index.js`)

### Inyección de Dependencias (Prohibición de Importaciones Internas)
- Queda **estrictamente prohibido** que la Vista, el Modelo o el Controlador importen dependencias o instancien partes de su propia triada directamente.
- Toda dependencia debe recibirse a través del `constructor()`.
- El **Factory** es el único archivo en cada componente autorizado para importar modulos, instanciar las clases y ensamblar las piezas o inyectar clases de otros componentes.
- *Gestión de APIs y Lógica Externa:* Dado que no existen servicios globales centralizados, cualquier conexión (ej. llamadas a la API de Gemini, Fetch general al Node Backend node) debe ejecutarse implementándose **directamente en el Modelo del componente** que lo necesita.

### Flujo de Datos Unidireccional
1. **Ensamblaje**: El Factory origina las instancias, creando primero el Modelo, luego la Vista (inyectándole el contenedor raíz DOM `this.root`), y por último el Controlador (inyectándole el Modelo y la Vista referenciadas).
2. **Inyección de Eventos**: El Controlador llama a la función mapeadora de la Vista para los eventos (ej. `bindSubmit(handler)`).
3. **Interacción y Mutación**: El usuario ejecuta una acción, el evento nativo del DOM ocurre, la Vista ejecuta el handler inyectado y transfiere la responsabilidad delegándola al Controlador.
4. **Respuesta**: El Controlador procesa el flujo, ordena al Modelo que se comunique con APIs externas o que almacene los datos (en LocalStorage) y, al recibir una promesa de éxito, manda la instrucción a la Vista de que actualice de forma "tonta" la interfaz de usuario.

## 3. Manejo de Nomenclaturas y Restricciones (Module ESM)

- **Agnosticismo de la Vista y el Modelo**: El Model no sabe de la existencia del objeto `document` o del HTML; toda modificación del DOM vive 100% en la View. Por contraparte, la View es ignorante a los detalles y condicionales de negocio del Model.
- **Exportaciones Nombradas ES6**: Absolutamente todas las clases deben ser exportadas de forma nombrada (ej. `export class ModelName`). El prefijo `export default` está prohibido para permitir un mejor rastreo y "Tree-shaking" de código en Vite.
- **Prefijo del Sistema DOM**: Cualquier valor dentro de clase `View` que mantenga como propiedad una referencia a un nodo explícito del DOM, está obligado a iniciar su nombre de variable con un `$` (signo de dólar), por ejemplo: `this.$form = ...`.

## 4. Renderizado Obligatorio (DOMParser)

Para asegurar consistencia, modularidad y seguridad, **todas las vistas** deben usar obligatoriamente explícitamente `DOMParser` para todo el renderizado. Cualquier inyección de nuevos elementos visuales al DOM debe hacerse mediante la construcción dinámica de strings (Template Literals) convirtiéndolos a nodos HTML con esta API en lugar de métodos como `innerHTML` directo en el documento o creaciones imperativas sueltas con `document.createElement`.

## 5. Gestión de Estilos CSS

El proyecto se regirá por una hoja de estilos globalizada. Debe existir un archivo llamado `styles.css` ubicado en la raíz del proyecto, en el cual estarán definidos todos los estilos CSS para todo el proyecto y todos sus componentes. Queda proscrito el uso de módulos CSS disgregados o archivos de estilos por carpeta de componente.
