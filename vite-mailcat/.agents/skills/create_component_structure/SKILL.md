---
name: create_component_structure
description: Skill obligatoria para implementar la estructura de carpetas inicial de un nuevo componente en el proyecto, previa consulta al usuario sobre el nombre.
---

# Creación de Estructura de Carpetas para Nuevo Componente

Cuando se requiera o el usuario solicite "crear un nuevo componente", iniciar el desarrollo de un componente o estructurar uno, **DEBES** utilizar esta skill de manera inmediata para la creación inicial de su entorno y directorios.

## 1. Confirmación de Nombre (MANDATORY: ALTO TOTAL)
Es un requisito **ESTRICTO y OBLIGATORIO** detenerte y validar el nombre del componente antes de realizar cualquier acción en el sistema de archivos:
- **Pregunta:** Debes preguntarle al usuario por el nombre deseado para el componente. (Ej. *"Para proceder con la creación de las carpetas, ¿qué nombre llevará el componente?"*).
- **Espera:** **NO DEBES AVANZAR** bajo ninguna circunstancia. Debes devolver el control al usuario y esperar su respuesta.

## 2. Formato del Nombre del Componente
Una vez recibida la respuesta del usuario, debes aplicar formato **PascalCase** al nombre del componente (Ej. `LoginForm`, `Dashboard`, `SideBar`, `ShoppingCart`).

## 3. Crear el Árbol de Directorios y Archivos Base
Todo nuevo componente se debe crear dentro de la carpeta global de componentes `src/components/` (debes verificar que `src/components/` exista, y si no, crearla en la raíz de la aplicación Vite).

Dentro de `src/components/`, crearás una carpeta principal con el nombre del componente validado: `src/components/{ComponentName}/`.

Dentro de esa nueva carpeta, **debes crear la siguiente estructura obligatoria**:

1. Directorio `Controller` y dentro de este un archivo `.gitkeep` vacío.
2. Directorio `Model` y dentro de este un archivo `.gitkeep` vacío.
3. Directorio `View` y dentro de este un archivo `.gitkeep` vacío.
4. Directorio `Icons` y dentro de este un archivo `.gitkeep` vacío.

**Ejemplo de árbol resultante para un componente 'LoginForm':**
```text
src/
└── components/
    └── LoginForm/
        ├── Controller/
        │   └── .gitkeep
        ├── Model/
        │   └── .gitkeep
        ├── View/
        │   └── .gitkeep
        └── Icons/
            └── .gitkeep
```

## 4. Complemento y Relación con el Patrón MVC
Ten en cuenta la arquitectura estricta del proyecto MailCat:
- Esta skill solo crea el "esqueleto" organizativo inicial en carpetas, pero el proyecto se rige por la estructuración de la directriz principal (ver `apply_mvc_pattern`).
- Asegúrate de dejar los `.gitkeep` completamente vacíos. Sirven únicamente para mantener las carpetas en el sub-árbol de control de versiones Git hasta que los archivos reales de código (el Controller.js, Model.js, View.js, Factory.js y módulos complementarios) sean escritos dentro de ellas.
