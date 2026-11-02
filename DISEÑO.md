# Autoescuela: brief de diseño

Plantilla `autoescuela` creada el 02/11/2026 a partir de `escuela-infantil` con `php artisan plantillas:nueva`
(de la base solo queda la estructura técnica: `site.ts`, `Base.astro`, `Imagen.astro`, SEO de base y formularios).
Este fichero se queda en el repo: es lo que lee quien (persona o agente) rediseñe la plantilla.

## Brief

- **Para quién**: autoescuelas y centros de formación vial (sectores `autoescuela`, `permiso-conducir`,
  `formacion-vial`, `carnet-moto`). Quien entra quiere saber qué permiso puede sacarse, cuánto cuesta, cuándo hay
  teórica y cómo matricularse.
- **Qué tiene que conseguir la web**: matrículas (formulario en «Matrícula») y llamadas o WhatsApp (barra fija en
  móvil). El precio del pack estrella se ve en la portada.
- **Tono y estilo** (`vivo`): claro, directo y con energía. Referencia sí: la señalización vial (señales redondas
  con aro, triángulos de advertencia, carteles azules con filete blanco, rayas discontinuas). Referencia no: el
  look de taller o de transporte (mayúsculas condensadas o cursivas, rayas de peligro, cortes en diagonal).
- **Concepto**: «la carretera». Cada banda es un tramo: asfalto con la raya amarilla, carriles para los packs, una
  carretera que cruza la ventana con los pasos como hitos, un panel de orientación con el horario.
- **Paleta de ejemplo**: primario `#14213d` (azul noche), acento `#ffc21a` (amarillo señal), fondo `#f6f5f0`
  (blanco roto), texto `#101a30`. Derivados con `color-mix`: `--asfalto` (primario + negro), `--amarillo-suave`,
  `--azul-suave`. Todo depende de las cuatro variables: aguanta otros colores del cliente.
- **Tipografía**: titulares en la rotulación vial del sistema (`Bahnschrift` en Windows, DIN en Mac, después
  Barlow/Roboto/system-ui) a 700, en minúsculas y con interletrado ajustado; títulos de portada de 2,8 a 7,2 rem.
  Antetítulos pequeños en mayúsculas con interletrado y una raya discontinua de color. Texto en `system-ui`.
- **Formas**: esquinas pequeñas (0,6 rem); botones con filete interior como un cartel; señales redondas (disco
  blanco con aro azul) para iconos y cifras; triángulo con la edad mínima; placa «L» como marca sin logo.
- **Ritmo de bandas**: portada oscura (foto) → franja de asfalto → permisos amarillo → packs asfalto → cómo
  funciona claro → horario amarillo suave con foto a sangre → flota azul noche con franja de fotos → resultados
  amarillo con foto a sangre → opiniones sobre foto oscurecida → preguntas claro → matrícula amarillo → contacto
  claro con plano a sangre → pie asfalto con raya amarilla.

## Apartados (en orden)

1. `hero`: foto a sangre de un coche en carretera (oscurecida abajo e izquierda), antetítulo, título enorme, texto,
   dos botones, disco de precio (`destacado`: titulo, precio, texto) y franja de carretera con 3 datos (`items`).
2. `permisos`: rejilla vial de 4 columnas (`permisos`: nombre, texto, precio, incluye «;», edad_minima, icono).
3. `packs`: carriles con rayas discontinuas; el destacado en amarillo con `etiqueta_destacado`
   (`packs`: nombre, texto, precio, incluye «;», destacado).
4. `proceso`: carretera de borde a borde con hitos numerados (`items`: titulo, texto, icono).
5. `horario`: foto del aula a sangre + panel de orientación (`horario`: dia, horas, clase), `nota`.
6. `flota`: franja de fotos de borde a borde (`items`: titulo, texto, imagen, icono).
7. `resultados`: cifras en señales redondas + foto a sangre (`items`: titulo = cifra, texto). Sin cifras no sale.
8. `opiniones`: foto de fondo oscurecida, una opinión grande y el resto en columna (`testimonios`).
9. `preguntas`: acordeón `details/summary`.
10. `matricula`: ventajas con check, nota, teléfono/WhatsApp y formulario en panel vial (permiso y pack en
    desplegables).
11. `contacto`: teléfono grande, datos con icono en señal redonda, formulario y plano a sangre.

## Fotos

8 fotos en `fotos.json` (hero 16:9, aula y pista 4:3, volante 16:9, flota 3:4): carretera comarcal con campos y
montañas, aula de teórica, pista de motos con conos, interior de coche, y los cuatro vehículos. Sin texto legible,
sin logotipos, sin matrículas legibles y sin personas.

## Qué no hacer

- Volver a la «caja centrada con tarjetas blancas»: todo son bandas y rejillas a todo el ancho.
- Cursivas, mayúsculas condensadas, rayas de peligro o diagonales (son de `transporte-mudanzas` y `taller-mecanico`).
- Formas de juguete, festones o esquinas muy redondeadas (son de `escuela-infantil`).
- Precios o cifras en los componentes: solo en `site.yaml`.

## Páginas propias (fichas)
Con la misma piel que la portada: cabecera y pie de la plantilla, migas (Inicio › Sección › Elemento), hero con la foto del
elemento (sin foto, su icono), `detalle` en párrafos, tabla de datos, caja de contacto, galería (`imagenes`) y otros elementos
de la misma lista.
