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
- 16 elementos con `data-animar` (títulos y grillas) revelados con
  `cubic-bezier(0.22, 1, 0.36, 1)` y retraso escalonado vía `--a`.
- Portada con foto y superposición azul, cinta de cifras, bienvenida,
  franja de valores con desplazamiento suave (iconos Font Awesome, se pausa
  al pasar el cursor), etapas (Cuna/Inicial/Primaria/Secundaria), directora,
  proceso de admisión en 4 pasos (Contacto inicial, Inscripción, Matrícula,
  ¡Bienvenidos!), noticias, testimonios "¿Qué nos diferencia?",
  banner "Pide información" y pie de página (la sección Contacto fue
  eliminada; los enlaces apuntan a #admision y los datos quedan en el pie).
- Paleta real de St. George's: azul colegial `#1c3057`, azul oscuro `#001a4d`,
  fondo claro `#e6eeff`, botones rojo `#c03227`, acento celeste `#a4cbcc`,
  blanco. Fuentes: Inter (texto) y Space Grotesk (títulos).
- Datos reales: dirección "Pasaje Los Gaviones Mz. 109b Lte 2", teléfono 945 454 081,
  14 años de trayectoria, 7 docentes, 3 niveles + cuna, directora Celia Jeannete
  Valerio Avila, colegio de Atalaya (Perú). Correo `contacto@mibuenpastor.edu` es provisional.
- Iconos: Font Awesome 6.5.2 vía CDN (iconos sólidos, no trazar finos). No copiar
  iconos/fuentes de stgeorges.edu.pe (copyright).

## Reglas del proyecto

- Empezar simple: primero el sitio público (fotos + publicaciones).
- Avanzar por etapas pequeñas y verificar cada una antes de continuar.
- Usar git: hacer un commit después de cada etapa lograda.
- No pagar por servicios: usar herramientas y hosting gratuitos.
- No copiar textos/fotos/código de otros colegios (solo replicar estructura/estilo).
- Servir localmente con `npx live-server --port=8080 --no-browser`.