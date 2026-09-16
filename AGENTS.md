# Proyecto MBPweb

Sitio web para el colegio **I.E.P Mi Buen Pastor**. Objetivos generales:

- Página pública con fotos y publicaciones del colegio.
- Sección de matrícula (inscripción de estudiantes).
- Intranet para estudiantes con inicio de sesión.

## Estado actual

Sitio público de una sola página (`index.html` + `style.css`) inspirado en la
estructura de St. George's College (stgeorges.edu.pe) con contenido original:

- Menú superior con megamenu (Foto + enlaces) en cada desplegable: Etapas
  educativas, Admisiones, Nuestro colegio, Noticias y eventos, Contacto.
- Portada con foto y superposición azul, cinta de cifras, bienvenida,
  carrusel de valores, etapas (Cuna/Inicial/Primaria/Secundaria), directora,
  proceso de admisión en 7 pasos, noticias, testimonios "¿Qué nos diferencia?",
  acreditaciones, banner "Pide información", contacto y pie de página.
- Paleta real de St. George's: azul colegial `#1c3057`, azul oscuro `#001a4d`,
  fondo claro `#e6eeff`, botones rojo `#c03227`, acento celeste `#a4cbcc`,
  blanco. Fuentes: Inter (texto) y Space Grotesk (títulos).
- Datos reales: dirección "Pasaje Los Gaviones Mz. 109b Lte 2", teléfono 945 454 081,
  14 años de trayectoria, 7 docentes, 3 niveles + cuna, directora Celia Jeannete
  Valerio Avila. Correo `contacto@mibuenpastor.edu` es provisional.

## Reglas del proyecto

- Empezar simple: primero el sitio público (fotos + publicaciones).
- Avanzar por etapas pequeñas y verificar cada una antes de continuar.
- Usar git: hacer un commit después de cada etapa lograda.
- No pagar por servicios: usar herramientas y hosting gratuitos.
- No copiar textos/fotos/código de otros colegios (solo replicar estructura/estilo).
- Servir localmente con `npx live-server --port=8080 --no-browser`.