# Software Requirements Specification (SRS) - MailCat

## 1. Resumen del Proyecto

MailCat es una aplicación web diseñada para transformar borradores de texto en correos electrónicos corporativos profesionales utilizando inteligencia artificial. El objetivo es proporcionar una herramienta rápida que garantice claridad, tono adecuado y corrección gramatical en la comunicación empresarial.

## 2. Arquitectura y Stack Tecnológico

Para garantizar la escalabilidad y un código limpio, el proyecto seguirá estas directrices:

- **Entorno de Desarrollo:** Vite.
- **Lenguaje:** Vanilla JavaScript (ES6+).
- **Patrón Arquitectónico:** MVC Estricto con Inyección de Dependencias (Factory).
  - **Regla de 4 Archivos:** Cada componente frontend constará exactamente de `Model.js`, `View.js`, `Controller.js` y `Factory.js` (o `index.js`).
  - **Inyección de Dependencias:** Queda estrictamente prohibido que el Modelo, la Vista o el Controlador importen dependencias o módulos internos directamente.
  - **Responsabilidad del Factory:** El `Factory` es el único archivo autorizado para importar, instanciar y ensamblar las partes del componente, inyectándolas vía constructores.
  - **Flujo de Datos Unidireccional:** El Controller maneja los eventos de la View, muta el Model y re-renderiza la View, garantizando una separación de responsabilidades sin acoplamiento.
- **Componentización:** La lógica debe estar aislada en componentes independientes:
  - **LoginComponent:** Gestión de acceso de usuarios.
  - **ValidatorComponent:** Validación de entradas de texto.
  - **StorageComponent:** Manejo de persistencia en SessionStorage.
  - **SidebarComponent:** Barra lateral de navegación y ajustes.

## 3. Requisitos Funcionales (Core Features)

El "cerebro" de la aplicación será Gemini 3 Flash, seleccionado por su velocidad y eficiencia en tareas de ingeniería de software.

**Capacidades de Transformación de IA:**

- **Crear:** Generar un correo desde cero a partir de puntos clave.
- **Generar con Meta:** Generar un correo electrónico enfatizando una meta específica o persuadiendo para lograrla, utilizando las mejores técnicas de negociación y aplicando psicología de negocios.
- **Formalizar:** Convertir lenguaje informal en un tono corporativo estándar.
- **Acortar:** Resumir correos extensos manteniendo la información crítica.
- **Cambiar Tono:** Ajustar la intención (ej. de directo/urgente a diplomático).
- **Corregir Gramática:** Limpieza técnica de sintaxis y ortografía.

## 4. Gestión de Datos y Backend

- **Servidor:** Node.js con Express.
- **Autenticación:** Sistema de login con una tabla de usuarios registrados.
- **Persistencia de Correos:** Durante el MVP, los correos procesados se guardarán exclusivamente en el LocalStorage del navegador del usuario.
- **Futuras Integraciones:** El diseño debe dejar la puerta abierta para la conexión con APIs de envío de correo (SMTP/Gmail) mediante protocolos MCP.

## 5. Interfaz y Guía de Estilo

- **Referencia de Diseño:** Toda la identidad visual, paleta de colores y componentes de UI se regirán por el documento `Design.md`.
