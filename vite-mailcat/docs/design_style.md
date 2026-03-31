# MailCat Design System & Style Guidelines para IA

**Propósito:** Este documento actúa como la fuente de verdad (Source of Truth) para la generación de código frontend por parte de Agentes IA. Cualquier componente, vista o layout que se genere para la aplicación MailCat DEBE cumplir estrictamente con estas reglas.

---

## 1. Filosofía de Diseño: Mobile-First y Jerarquía Tonal
*   **Mobile-First Estricto:** Todos los estilos deben definirse primero para móviles. Utiliza variables CSS, Flexbox y CSS Grid para expandir el layout fluidamente hacia resoluciones de escritorio.
*   **The "No-Line" Rule:** PROHIBIDO el uso de bordes sólidos de 1px (como `border: 1px solid #ccc;`) para seccionar el layout. Las delimitaciones entre paneles o sidebars deben lograrse a través de la diferencia tonal de los fondos ("background color shifts" y contenedores anidados).
*   **Asimetría Controlada:** Prioriza el espacio en blanco ("breathing room") para reducir la carga cognitiva. Usa un "Stage" o escenario para evitar el efecto de "cajas amontonadas".

---

## 2. Tipografía (El Toque Editorial)
*   **Fuente Única:** `Inter`, Sans-Serif. Debe usarse siempre con antialiasing (`antialiased`) y tracking ajustado (`tracking-tight`).
*   **Jerarquía de Tamaños y Pesos:**
    *   **H2 (Títulos Principales):** 32px a 40px (Desktop), *Bold* (700). Deben ir centrados en el Dashboard principal.
    *   **Textos de Cuerpo / Botones (Cuerpo):** 14px a 16px. *Medium* (500) o *Semibold* (600) para elementos interactuables. Line-height enfocado a la legibilidad.
    *   **Etiquetas / Metadata (UI Text):** 12px a 13px. Útil para indicar estados secundarios, labels superiores, o detalles adjuntos.

---

## 3. Tema Claro (Slate & Indigo) - Default
*   **Fondo de Aplicación Principal:** `#F8FAFC` (Slate 50 / Blanco Nieve).
*   **Fondo de Contenedores y Tarjetas:** `#FFFFFF` (Blanco puro para dar un efecto de "papel elevado").
*   **Color de Acento Principal:** `#5a7dfa` (Azul Índigo Suave).
*   **Texto Principal:** `#1E293B` (Slate 800) - ¡NO usar negro puro!
*   **Degradado Primario (Botones y CTAs en foco):** `linear-gradient(135deg, #5a7dfa 0%, #3b5bdb 100%)`.
*   **Regla de Focus en Inputs:** Sin bordes por defecto (relleno gris claro). En foco, fondo blanco y subrayado inferior de 2px color Indigo (no un borde completo).

---

## 4. Tema Oscuro (Emerald Intelligence) - Opcional/Alterno
*   **Fondo de Aplicación Principal:** `#0e0e0e` (Negro Mate profundo).
*   **Fondo de Contenedores y Tarjetas:** `#1a1a1a` o `#201f1f`.
*   **Color de Acento Principal:** `#59de9b` (Verde Esmeralda Vibrante).
*   **Color sub-Acento (Botones sec):** `#00A86B`.
*   **Texto Principal:** `#E5E2E1` (Gris Platino).
*   **Degradado Primario (Botones y CTAs en foco):** `linear-gradient(135deg, #59de9b 0%, #00A86B 100%)`.

---

## 5. UI Kit y Geometría
*   **Radios de Borde (Border Radius):**
    *   **Tarjetas y Bloques Generales:** `16px`.
    *   **Botones y Campos de Entrada (Inputs):** Forma de píldora (Completamente redondeados / `border-radius: 9999px`) o `12px` dependiendo de la densidad y el contexto. Mantener esto sincronizado en ambos temas.
*   **Elevación y Profundidad:**
    *   El sombreado "Shadow-heavy" está desaconsejado. Usa la diferencia de elevación por color (`#F8FAFC` detrás de una tarjeta `#FFFFFF`) y ocasionalmente fondos de cristal (Opacidad 80% + Backdrop Blur de 20px) flotantes.
*   **Botones de Acción Principales (CTAs):**
    *   Altura Fija: `60px`.
    *   Efectos obligatorios: Sombra base suave (`box-shadow`), al presionar escalar ligeramente el botón a 0.95 (`transform: scale(0.95)`), con transiciones suaves aplicadas.

---

## 6. Layout Base del Dashboard Principal (MailCat)
*   **Estructura Global:**
    *   **Sidebar (Escritorio):** Fijo a `256px` de ancho, altura de `100vh`. En versión móvil, oculto o accesible mediante menú de hamburguesa.
    *   **Topbar (Header):** Altura fija de `60px` (Si aplica).
*   **Zona de Trabajo (Estructura a dos filas en Desktop):**
    *   **Fila 1 (Entrada de texto):** Compuesta por 2 columnas.
        *   *Columna Izquierda (Workspace Principal):* Contiene el "Input Draft", un área de texto con altura dinámica y alineación inferior conectada a la base de la columna derecha. Este es el "Editor Card" principal.
        *   *Columna Derecha (Controles y IA):* Aloja el botón Principal CTA "Optimizar con IA" fijado arriba (altura `60px`), seguido por debajo de selectores de configuración en formato Chips ("Parámetros de Tono") con estados activos/inactivos muy diferenciados.
    *   **Fila 2 (Salida):**
        *   *Contenedor de Resultados (Synthesis Result):* Situado por debajo, requiere un mínimo de `400px` de altura para mostrar los borradores generados.

---

## 7. Animaciones y Micro-Interacciones
*   **Transiciones Universales:** Siempre usa la curva `ease-in-out` con duración de `0.3s` para estados de hover, active y visibilidad (ej. `transition: all 0.3s ease-in-out;`).
*   **Estado Hover (Desktop):** Cambios sutiles de opacidad en botones secundarios o un leve incremento en el sombreado blur en tarjetas.
*   **Indicadores de AI Generating:** En el logotipo principal "Engine Status" se debe aplicar una animación de latido/pulso continuo y suave para indicar que "la IA está pensando / generando el correo".
