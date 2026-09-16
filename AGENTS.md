# Proyecto MBPweb

Sitio web para el colegio **I.E.P Mi Buen Pastor**. Objetivos generales:

- Página pública con fotos y publicaciones del colegio.
- Sección de matrícula (inscripción de estudiantes).
- Intranet para estudiantes con inicio de sesión.

## Estado actual

Sitio público de una sola página (`index.html` + `style.css`) inspirado en la
estructura de St. George's College (stgeorges.edu.pe) con contenido original:

- Menú superior con desplegables (Etapas educativas, Admisiones, Nuestro colegio,
  Noticias y eventos) más iconos de ubicación, portal e idioma.
- Animaciones: entrada de secciones al hacer scroll (IntersectionObserver +
  @keyframes), entrada del hero, transiciones suaves en hover de tarjetas,
  imágenes, pasos, enlaces, botones y subrayado animado del menú.
  Respetan `prefers-reduced-motion`.
- Convenciones de animación (aplicar SIEMPRE en index y páginas nuevas):
  - Animar solo `transform` y `opacity` (nunca top/margin/width/height).
  - Entradas de 300-500 ms con `cubic-bezier(0.22, 1, 0.36, 1)` y
    `animation-fill-mode: both`.
  - Grillas con aparición escalonada: clase `grid-animada` en el contenedor
    (con `data-animar`); cada hijo se revela con 90 ms de retraso vía nth-child.
  - Usar transiciones para hovers de 2 estados (no @keyframes); prohibido
    `transition: all`.
  - CTA principal con clase `atencion`: anillo pulsante (solo opacity) que
    desaparece al hacer clic (JS agrega `.toggled`).
  - Foco visible para teclado: `:focus-visible` global.
  - `prefers-reduced-motion: reduce` = quitar animación, dejar estado final
    visible (el anillo CTA queda estático).
  - 16 elementos con `data-animar` (títulos y grillas) revelados con
  `cubic-bezier(0.22, 1, 0.36, 1)` y retraso escalonado vía `--a`.
- Portada con foto y superposición azul, cinta de cifras, bienvenida,
  franja de valores con desplazamiento suave (iconos Font Awesome, se pausa
  al pasar el cursor), etapas (Cuna/Inicial/Primaria/Secundaria), directora,
  proceso de admisión en 4 pasos (Contacto inicial, Inscripción, Matrícula,
  ¡Bienvenidos!), noticias, testimonios "¿Qué nos diferencia?",
  banner "Pide información" y pie de página (la sección Contacto fue
  eliminada; los enlaces apuntan a #admision y los datos quedan en el pie).
- Paleta del sitio "Marino" (elegida por opencode, tema oceánico):
  - Marino `#0E4D64` (primario: botones, iconos acento, overlays de fotos),
    marino vivo `#16708F` (hovers), marino oscuro `#0A3A4C` (hover botones).
  - Aguamarina `#2A9D8F` (acento secundario de marca, scrollbar) y espuma
    `#A8DFE3` (turquesa claro para texto/iconos o botones sobre fondos marino).
  - Neutros fríos: tinta `#16313F` (textos/footer/overlays), tinta suave
    `#4F6875` (texto secundario), bruma `#F4FAFB` (fondos claros),
    bruma suave `#E4F0F2` (fondos alternos), borde `#C9DFE2`, blanco.
    Variables en `:root` de `style.css`: `--marino`, `--marino-vivo`,
    `--marino-oscuro`, `--aguamarina`, `--espuma`, `--tinta`, `--tinta-suave`,
    `--bruma`, `--bruma-suave`, `--borde`, `--blanco`, `--sombra`,
    `--sombra-fuerte`. Fuentes: Inter (texto) y Space Grotesk (títulos).
- Datos reales: dirección "Pasaje Los Gaviones Mz. 109b Lte 2", teléfono 945 454 081,
  12 años de trayectoria (desde 2014, calculado a 2026), 7 docentes, 3 niveles + cuna, directora Celia Jeannete
  Valerio Avila, colegio de Atalaya (Perú). Correo de contacto oficial Gmail `i.e.pmibuenpastor@gmail.com`
  (destino de las inscripciones vía FormSubmit).
- Inscripciones externas: `matricula.html` usa FormSubmit.co (gratis, sin backend) hacia
  `i.e.pmibuenpastor@gmail.com`; la primera vez se activa con un correo de confirmación
  (revisar Spam) y luego cada solicitud llega como correo con tabla de datos.
- Iconos: Font Awesome 6.5.2 vía CDN (iconos sólidos, no trazar finos). No copiar
  iconos/fuentes de stgeorges.edu.pe (copyright).
- Páginas por etapa: cada nivel tiene su propia página (`cuna.html`,
  `inicial.html`, `primaria.html`, `secundaria.html`). Todas comparten
  `style.css` con clases `.pagina-*` y los enlaces "Saber más" de cada tarjeta
  llevan a su página.
- Fotos propias: `fotos/hero/` (fondo rotativo del hero, `hero-N.jpg`),
  `fotos/galeria/` (galería/uso general, `galeria-N.jpg`), `fotos/directora.jpg`
  y fotos de etapas (`cuna.jpg`, `portada-inicial.jpg`, `primaria.jpg`,
  `secundaria.jpg`). El hero referencia `hero-5..hero-7.jpg`; la imagen lateral
  del colegio usa `fotos/galeria/galeria-1.jpg`.
- Logos oficiales del colegio (propios del colegio, sin copyright):
  - Fuente original en `MiPastor Since 2014/` (PNG, JPG, Editables .ai/.eps).
  - Copias web en `logos/`: `logo-horizontal.png` (color, sobre blanco),
    `logo-horizontal-negativo.png` (blanco, sobre navy), `logo-vertical-negativo.png`
    (blanco, logo girando en la transición). Se usan en encabezado (`.marca-logo`),
    pie (`.footer-logo`) y overlay de carga (`.escudo`), reemplazando el texto
    y el escudo SVG dibujado a mano.
  - Colores reales de la marca: bordo `#802927` y beige/arena `#927A56`
    (solo quedan en el logo; la paleta del sitio es la "Marino").

## Reglas del proyecto

- Empezar simple: primero el sitio público (fotos + publicaciones).
- Avanzar por etapas pequeñas y verificar cada una antes de continuar.
- Usar git: hacer un commit después de cada etapa lograda.
- No pagar por servicios: usar herramientas y hosting gratuitos.
- No copiar textos/fotos/código de otros colegios (solo replicar estructura/estilo).
- Servir localmente con `npx live-server --port=8080 --no-browser`.
- `.marca` (encabezado) y `.footer-marca`: usan imágenes en `logos/`; no volver
  a texto/svg salvo que el usuario lo pida.