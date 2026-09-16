# Proyecto MBPweb

Sitio web para el colegio **I.E.P Mi Buen Pastor**. Objetivos generales:

- Página pública con fotos y publicaciones del colegio.
- Sección de matrícula (inscripción de estudiantes).
- Intranet para estudiantes con inicio de sesión.

## Estado actual

Sitio público de una sola página (`index.html` + `style.css`) inspirado en la
estructura de St. George's College (stgeorges.edu.pe) con contenido original:

- Menú superior con desplegables (NIVELES EDUCATIVOS, Admisiones, Nuestro colegio,
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
  al pasar el cursor), niveles educativos (Cuna/Inicial/Primaria/Secundaria),
  palabras de la directora, noticias, banner "Pide información" y pie de página.
  La sección de niveles se llama "NIVELES EDUCATIVOS" (sin subtítulo ni intro;
  solo título + tarjetas). La sección de noticias se llama "NOTICIAS Y EVENTOS"
  (en mayúsculas, sin subtítulo; solo título + tarjetas).
- Noticias con panel CMS (Decap CMS, gratis y de código abierto):
  - Las noticias ya no son HTML fijo: viven en `noticias.json` y `index.html`
    las dibuja con un pequeño script (construye las tarjetas con las clases
    `.noticia`, `.noticia-imagen`, `.noticia-cuerpo`, `.fecha`, `.enlace`;
    usa `textContent`, respeta el retraso escalonado de la grilla y formatea
    la fecha ISO a "día de mes de año" en español).
  - Si el `fetch` de `noticias.json` falla (p. ej. página abierta por
    `file://`), se muestran 3 noticias de respaldo embebidas en el JS.
  - `admin/index.html` + `admin/config.yml` cargan el panel en
    `http://sitio/admin`. Configuración: backend `git-gateway` rama `main`,
    colección tipo *file* apuntando a `noticias.json` (lista de noticias con
    título, fecha, imagen y resumen). `media_folder: fotos/noticias`,
    `public_folder: /fotos/noticias` (las fotos subidas van a `fotos/noticias/`).
  - Para publicar, la directora o un editor entra a `<sitio>/admin`, inicia
    sesión (Netlify Identity), escribe/edita noticias y "Publica"; Decap hace
    commit al repo y Netlify redespliega por sí solo (sin build: el sitio es
    estático vanilla).
  - Falta por hacer (pasos manuales del usuario): subir el repo a GitHub,
    conectar Netlify al repo (hosting gratis), activar `Identity` + `Git
    Gateway` y entonces se puede invitar editores por correo. El `fetch` de
    `noticias.json` no funciona al abrir por `file://`, solo servido por HTTP.
- La sección "El colegio" fusiona bienvenida y directora: dos párrafos de
  bienvenida (sin foto lateral, se quitó galeria-1.jpg) seguidos del bloque
  `#directora` con la foto de la directora a la izquierda y sus palabras.
- El home se mantiene minimalista: el proceso de admisión (4 pasos) y los
  testimonios se quitaron del home y viven en sus propias páginas/secciones
  (admision.html y secciones futuras del megamenú). Todos los enlaces que
  apuntaban a `#admision` ahora apuntan a `admision.html`.
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
  - Envío con `fetch` al endpoint AJAX `https://formsubmit.co/ajax/...` (NO `data-ajax`):
    la página no redirige, oculta el form y muestra el mensaje de confirmación en el lugar.
    FormSubmit ya activado por el usuario en su Gmail.
  - Validación: `required` en todos los campos obligatorios (bloquea el envío);
    único campo opcional es `comentarios`. El `submit` llama `form.reportValidity()`.
  - Selector de nivel (Cuna/Inicial/Primaria/Secundaria) → campo grado dinámico
    (`gradosPorNivel` en JS): Cuna [1-3 años], Inicial [3-5 años], Primaria [1º-6º],
    Secundaria [1º-5º].
  - Tipo de responsable (Padre/Madre/Apoderado/a/Ambos): al elegir un tipo se muestra
    `#datosResponsable` con etiqueta dinámica (`#labelNombreResponsable`:
    "...del padre", "...de la madre", "...del apoderado"); con "Ambos" se muestra además
    `#bloqueSegundo` (etiqueta "...de la madre"). Los campos del segundo responsable se
    limpian, deshabilitan y dejan de ser `required` si NO se elige "Ambos" (así no llegan
    vacíos al correo).
  - Celular: un solo campo con `select` de país + input de número lado a lado
    (`.telefono-fila`); las opciones muestran solo código + prefijo: "PE +51", "AR +54",
    "BO +591", "CL +56", "CO +57", "CR +506", "EC +593", "ES +34", "US +1", "GT +502",
    "MX +52", "NI +505", "PA +507", "PY +595", "VE +58".
  - Grid `.campos` de 2 columnas; `#datosResponsable` ocupa todo el ancho
    (`grid-column: 1 / -1`) y es un sub-grid de 2 columnas; `[hidden]{display:none!important}`
    para `.datos-responsable` y `.bloque-segundo`.
  - Lista `.inscripcion-lista` (sidebar "Únete a la familia"): los 4 niveles son
    enlaces `.nivel-boton` (botones clicables con hover) que llevan a las páginas de
    cada etapa: Cuna→`cuna.html`, Inicial→`inicial.html`, Primaria→`primaria.html`,
    Secundaria→`secundaria.html`.
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
- La página pública se mantiene SIEMPRE en HTML/CSS/JS vanilla (sin React,
  Tailwind ni build). Para componentes o animaciones vistos en otros proyectos
  (por ej. Rare UI), copiar la idea y portarla a CSS/JS vanilla: mismo efecto
  visual, sin la complejidad. La intranet/aula virtual futura sí podrá usar
  React y su propio stack.