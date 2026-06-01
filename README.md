# 🏛️ Magna Propiedades

**Magna Propiedades** es un portal web inmobiliario de alta gama y diseño editorial de lujo, desarrollado a medida para el mercado de la Patagonia Argentina (Trelew, Rawson, Puerto Madryn y alrededores).

El sitio web está concebido bajo una estética minimalista premium en tonos claros y cálidos (Beige, Warm Sand y Soft Sage), priorizando la legibilidad, las transiciones sutiles y una experiencia de usuario sumamente inmersiva y de alta fidelidad, inspirada en las publicaciones editoriales de arquitectura y diseño internacional.

---

## 🎨 Principios de Diseño e Identidad

*   **Estética Editorial de Lujo:** Uso exclusivo del maridaje tipográfico entre **Playfair Display** (títulos con serif clásica y elegante) e **Inter** (cuerpo y datos sans-serif geométricos legibles).
*   **Modo Claro Consistente (Modo Claro Exclusivo):** No se utilizan alternadores de modo oscuro. Toda la interfaz reposa en una base suave color crema (`#fdfcf9`) con bordes de Warm Sand (`#f2ede4`) y contrastes intensos en Dark Olive (`#0a2013`).
*   **Enfoque de Conversión Directa (Sin Exposición de Precios):** Para resguardar la privacidad y potenciar la interacción comercial de alto nivel, se eliminaron por completo las etiquetas públicas de precios. Las conversiones e interesados se canalizan de forma instantánea a través de botones de llamado a la acción integrados con mensajes pre-redactados personalizados hacia **WhatsApp**.
*   **Experiencia Táctil e Interacciones Premium:** Integración fluida de carruseles de deslizamiento Swiper, grillas asimétricas responsivas y animaciones sutiles de entrada (`fadeInUp` y `fadeIn`).

---

## 🛠️ Stack Tecnológico

1.  **Core Framework:** [Astro (SSG)](https://astro.build/) para una velocidad de carga ultrarrápida a través de generación de páginas estáticas e hidratación selectiva de scripts en el cliente.
2.  **Maquetación y Estilos:** [Tailwind CSS v4](https://tailwindcss.com/) siguiendo estrictamente las pautas de [SKILL.md](file:///d:/code/magna-propiedades/SKILL.md), centralizando todos los tokens semánticos (colores, sombras, redondeados premium) dentro de la directiva `@theme` en `src/styles/global.css` para evitar el uso de clases inline arbitrarias.
3.  **Librería de Deslizamiento:** [Swiper](https://swiperjs.com/) para las galerías táctiles de dispositivos móviles y sliders interactivos de ampliación.
4.  **Lógica del Lado del Cliente:** JavaScript de alto rendimiento (Vanilla JS) sin necesidad de frameworks de JS pesados, garantizando un rendimiento óptimo de SEO y accesibilidad.

---

## 📁 Estructura y Arquitectura del Proyecto

```text
/
├── public/                     # Recursos estáticos (favicon, iconos)
├── src/
│   ├── components/             # Componentes modulares premium
│   │   ├── CustomSelect.astro  # Menú desplegable interactivo personalizado de lujo
│   │   ├── FilterBar.astro     # Barra de filtros horizontales de catálogo
│   │   ├── Footer.astro        # Pie de página institucional editorial
│   │   ├── Header.astro        # Cabecera sticky glassmorphic con menú de navegación móvil
│   │   ├── Hero.astro          # Sección principal de bienvenida con buscador rápido integrado
│   │   ├── PropertyCard.astro  # Tarjeta de inmueble en grilla con botón de ancho completo
│   │   ├── PropertyGallery.astro # Grilla de fotos asimétrica (21/9) y swiper móvil
│   │   ├── ServicesIntegrales.astro # Secciones de servicios de arquitectura/legal/limpieza
│   │   └── ServicesProfessionals.astro # Tarjetas de servicios principales (tasación/administración)
│   ├── data/
│   │   └── propiedades.json    # Modelo de datos unificado de las propiedades activas
│   ├── layouts/
│   │   └── Layout.astro        # Envoltura base HTML5 con SEO metadata y fuentes tipográficas
│   ├── pages/
│   │   ├── propiedades/
│   │   │   └── [id].astro      # Ficha técnica individual interactiva (Rutas dinámicas)
│   │   ├── catalogo.astro      # Catálogo estático con búsqueda y filtrado dinámico en tiempo real
│   │   └── index.astro         # Página de aterrizaje editorial (Home)
│   └── styles/
│       └── global.css          # Estilos globales y tokens semánticos de marca en Tailwind v4
├── package.json
└── README.md
```

---

## 💎 Características e Innovaciones Técnicas

### 1. Selectores Personalizados Premium (`CustomSelect.astro`)
En lugar de menús de selección nativos del navegador, implementamos un componente desplegable a medida:
*   **Posicionamiento Exacto e Inmune:** El panel de opciones utiliza `absolute top-full mt-1 left-0 right-0 z-35` dentro de una envoltura relativa, asegurando que siempre se abra exactamente debajo del botón gatillador, libre de interferencias del label del campo.
*   **Estilo Glassmorphic de Lujo:** Fondo difuminado semi-transparente con desenfoque de fondo (`backdrop-blur-md bg-white/95`) y transiciones fluidas de deslizamiento y escala (`origin-top scale-95` a `scale-100`).
*   **Intercepción Reactiva de `.value` (Painless Integration):** Mediante `Object.defineProperty` en el input oculto nativo, el selector detecta cualquier cambio a su valor realizado programáticamente por otros scripts de la página (como al presionar "Limpiar Filtros" o al leer Query Params en la URL), sincronizando inmediatamente el texto visual de la etiqueta e iluminando la opción seleccionada.

### 2. Visor Ampliado Multidimensional y Simétrico (`[id].astro`)
Al hacer clic en cualquier imagen o miniatura de la propiedad, se despliega una visualización inmersiva:
*   **Bypass de Contexto de Apilamiento:** Forzamos la presentación a pantalla completa mediante estilos inline de alta prioridad (`position: fixed !important; z-index: 99999 !important; inset: 0px !important;`), evitando que cabeceras fijas o animaciones en el cuerpo de la página sangren por encima.
*   **Alineación Simétrica de Flechas:** Las flechas del carrusel Swiper se colocaron fuera de los límites de la imagen, alineándose de forma absoluta respecto al ancho del viewport (`left-4 md:left-8` y `right-4 md:right-8` con `top-1/2 -translate-y-1/2`), luciendo idénticas en estilo circular de lujo al botón de cerrado superior.
*   **Compensación de Reflow:** El script implementa un retardo de `50ms` (`setTimeout`) al abrirse el visor para dar tiempo al navegador a refaccionar la grilla y permitir que Swiper calcule su tamaño de pixelaje ideal, logrando centrar los slides perfectamente.

### 3. Filtros del Catálogo Instantáneos (`catalogo.astro`)
*   La barra de filtros ejecuta búsquedas instantáneas y sin recargas en el cliente. Filtra por Operación (Venta/Alquiler), Tipo de Propiedad y Ciudad.
*   Si no se encuentran coincidencias, el sistema ofrece un estado de vacío minimalista que permite reiniciar todos los filtros de manera instantánea regresando los selects personalizados a su estado por defecto.

### 4. Integración de Ubicación por Google Maps Embebido
*   Integramos un mapa de Google Maps interactivo básico mediante `<iframe>` dinámico generado a partir de la dirección y ciudad registradas en el JSON.
*   El mapa está enmarcado estéticamente (`rounded-xl border border-brand-sand shadow-inner w-full aspect-[16/10]`) y matizado con un filtro sutil en escala de grises y contraste para que armonice perfectamente con los tonos naturales y beiges del portal inmobiliario.

---

## 🚀 Comandos del Desarrollador

Los comandos se corren desde la raíz del proyecto usando `pnpm`:

| Comando | Acción |
| :--- | :--- |
| `pnpm install` | Instala las dependencias y la librería Swiper en el entorno local |
| `pnpm dev` | Levanta el servidor de desarrollo local en `http://localhost:4321` |
| `pnpm build` | Compila y genera el sitio estático optimizado de producción dentro de `./dist/` |
| `pnpm preview` | Previsualiza localmente el build de producción antes del despliegue en servidor |
| `pnpm astro ...` | Ejecuta comandos nativos de la interfaz de comandos (CLI) de Astro |
