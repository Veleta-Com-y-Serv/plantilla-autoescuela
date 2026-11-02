# Plantilla «Autoescuela» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **vivo**.
Todo en castellano de España, frases cortas, sin jerga. El diseño y su porqué están en `DISEÑO.md`.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa (con las listas propias `permisos` y `packs`); no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario = azul noche, acento = amarillo señal, fondo = blanco roto, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…, y calcula `--c-sobre-primario`/`--c-sobre-acento`) y Tailwind los expone como `bg-primario`, `text-acento`… Derivados con `color-mix` en `src/styles/global.css`: `--asfalto` (primario casi negro: franja del hero, packs, opiniones, pie), `--amarillo-suave`, `--azul-suave`, `--linea` y `--blanco`.
- **Tipografía y aspecto general**: `src/styles/global.css`. Titulares en la rotulación vial del sistema (`Bahnschrift` en Windows, DIN en Mac; si no, la del sistema) a peso 700 y en minúsculas; texto en `system-ui`. Bandas `.banda` + `.banda-amarilla | -noche | -asfalto | -clara | -suave`; raya vial discontinua `.marca-vial` (y la de arriba del pie y de la franja del hero); botones con filete interior `.btn` (primario), `.btn-amarillo`, `.btn-sec`; señales: `.senal-redonda` (disco blanco con aro, `--aro` para cambiar su color), `.disco` (precio de la portada), `.triangulo` (edad mínima), `.panel-vial` (cartel azul con filete blanco), `.placa` (la «L» de la marca); `.rejilla-vial` (permisos), `.carriles` (packs), `.ruta`/`.hito` (cómo funciona), `.fila-sangre` (foto/texto 50/50 a sangre), `.franja`/`.vehiculo` (flota), `.cifras` (resultados), `.faq`, `.barra-movil`. Cabecera `.cabecera--placa` y pie `.pie--asfalto`. Sin fuentes externas.
- **Imágenes**: en `public/`. En `site.yaml` con ruta absoluta (`/fotos/hero.jpg`). Las fotos de la demo se generan a partir de `fotos.json`; mientras una foto `/fotos/x.jpg` no exista, `Imagen.astro` usa su respaldo `/placeholders/x.svg`. Las fotos nuevas del cliente van en `public/fotos/`.
- **Personas**: si se añaden (`personas[].foto` en un apartado nuevo), silueta `/placeholders/persona.svg` salvo foto del cliente. No se generan caras.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = placa «L» + nombre en texto.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie`.

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`, en el orden de `site.yaml`. `hero` y `contacto` son obligatorias. Todas son bandas a todo el ancho de la ventana.
- `hero` → `secciones/hero.astro` (foto a sangre de carretera, título enorme, disco de precio y franja de carretera con datos)
- `permisos` → `secciones/permisos.astro` (amarilla; rejilla vial de 4 columnas con señal, edad mínima en triángulo y precio en placa)
- `packs` → `secciones/packs.astro` (asfalto; carriles separados por rayas discontinuas; el destacado en amarillo)
- `proceso` → `secciones/proceso.astro` (clara; carretera de borde a borde con hitos numerados; vertical en móvil)
- `horario` → `secciones/horario.astro` (amarilla suave; foto del aula a sangre 50/50 y panel de orientación con las clases)
- `flota` → `secciones/flota.astro` (azul noche; franja de fotos de borde a borde sin margen)
- `resultados` → `secciones/resultados.astro` (amarilla; cifras en señales redondas y foto a sangre)
- `opiniones` → `secciones/opiniones.astro` (foto de fondo oscurecida; una opinión grande y las demás en columna)
- `preguntas` → `secciones/preguntas.astro` (clara; acordeón `details/summary`)
- `matricula` → `secciones/matricula.astro` (amarilla; ventajas y formulario en panel vial)
- `contacto` → `secciones/contacto.astro` (clara; teléfono grande, datos, formulario y plano a sangre)
- Diseño extra para apartados nuevos: `texto` (genérico; con imagen, fila 50/50 a sangre).

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, teléfonos, horarios, precios, fotos**: solo en `site.yaml`. Si un texto contiene comas o dos puntos dentro de `{ … }`, ponlo entre comillas. **Precios siempre como cadena** (`precio: "desde 390 €"`); precio vacío = no se muestra.
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Varios valores en una cadena separada por «;» (`incluye: "Matrícula; Teórica; 20 prácticas"`). Máximo 24 elementos por lista.
5. **Página nueva**: crea `src/pages/<slug>.astro` con `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu`. Ejemplo: `src/pages/aviso-legal.astro`.
6. **Apartado nuevo**: añade `secciones.<id-nuevo>` en `site.yaml` con `tipo:` igual al diseño que quieras (`texto`, `permisos`, `packs`, `proceso`, `horario`, `flota`, `preguntas`…). Si ninguno sirve, crea `src/components/secciones/<id>.astro` copiando la estructura de uno existente (`seccion(Astro.props.id)`, una `<section class="banda banda-…">`, `Titular`). `src/pages/index.astro` lo recoge solo: no lo toques.
7. **No tocar** `src/layouts/Base.astro`, `src/pages/index.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt). `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real, 16 px de margen lateral del texto (`.contenedor` o `--margen-panel`), las bandas y fotos a sangre de borde a borde y sin scroll horizontal en móvil (las bandas llevan `overflow-x: clip`). Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altSeccion` de `src/lib/seo.ts`); las decorativas, `alt=""`.
9. Los formularios no tienen servidor: abren el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro` y en `matricula.astro`.
10. Nunca inventes precios, cifras, opiniones ni datos que el cliente no haya dado: deja el campo vacío o la lista vacía (los componentes lo ocultan).

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Campos propios de esta plantilla (además del esquema común)
- `hero.destacado` {titulo, precio, texto}: disco de precio sobre la foto (sin precio no sale). `hero.items[]` {titulo, icono}: datos rápidos en la franja de carretera. `hero.cta` y `hero.cta_secundario`.
- `permisos.permisos[]`: `{ nombre, texto, precio, incluye, edad_minima, icono }` (`incluye` separado por «;»). `permisos.cta`: botón de cada permiso.
- `packs.packs[]`: `{ nombre, texto, precio, incluye, destacado }`. `packs.etiqueta_destacado`: cartel del pack destacado. `packs.cta`: botón de cada pack.
- `proceso.items[]` {titulo, texto, icono}: pasos (el número sale solo). `proceso.cta` opcional.
- `horario.horario[]` {dia, horas, clase}: clases de teórica (también salen en el horario de Google). `horario.nota`, `horario.imagen`, `horario.cta`.
- `flota.items[]` {titulo, texto, imagen, icono}: vehículos.
- `resultados.items[]` {titulo = la cifra, texto}, `resultados.imagen`. Sin cifras no se pinta.
- `opiniones.testimonios[]` {texto, autor, detalle}, `opiniones.imagen` (fondo). Sin opiniones no se pinta.
- `preguntas.preguntas[]` en acordeón; `preguntas.cta` opcional.
- `matricula.items[]` {titulo, texto}: ventajas con check. `matricula.nota`, `matricula.boton`. Formulario: nombre, email, teléfono, permiso y pack (desplegables con los `nombre` de `permisos` y `packs` de las secciones activas), fecha de nacimiento, turno y mensaje.
- `contacto.imagen`: plano a sangre que enlaza a mapas (sin plano, el formulario pasa a la derecha). `contacto.boton`.
- Barra móvil «Llamar / WhatsApp»: sale sola con `contacto.telefono` y/o `contacto.whatsapp`.
- Iconos disponibles (`icono:`): los de `src/components/ui/Icono.astro` (p. ej. `coche`, `moto`, `ciclomotor`, `camion`, `volante`, `semaforo`, `cono`, `carretera`, `senal`, `test`, `llave`, `ruta`, `lapiz`, `reloj`, `check`).

## Páginas propias (fichas por elemento)
- Listas con página propia (espejo de `fichas:` de template.yaml en `src/data/fichas.ts`): `secciones.permisos.permisos` → `/permisos/<slug>/` (permiso).
  **Solo los elementos con `detalle`** (texto largo, párrafos separados por una línea en blanco, ≤ 3000 caracteres, sin HTML) tienen página;
  los demás siguen como hasta ahora. Campos opcionales del elemento: `slug` (si falta, sale del nombre; no lo pongas sin motivo)
  e `imagenes` («/fotos/a.jpg; /fotos/b.jpg», galería de la ficha; la foto principal es `imagen` o, si no hay, la primera de `imagenes`).
  El resto de campos (precio, duración…) salen en la tabla de datos de la ficha.
- Una orden «añade una página para X» = escribir su `detalle` en site.yaml. Nunca crees a mano páginas en
  `src/pages/permisos/`: salen solas de `src/pages/[coleccion]/[slug].astro`.
- No tocar `src/lib/paginas.ts`, `src/lib/slug.ts` ni `src/lib/seo.ts` (comunes a todas las plantillas). Las páginas propias entran solas en
  `sitemap.xml` y `llms.txt`, con su JSON-LD (migas y servicio/producto con precio si lo hay).
