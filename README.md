# Plantilla NoExpertise · Autoescuela

Web viva para autoescuelas, con permisos, packs con precio, horario de teórica, flota y matrícula.

- Sectores: autoescuela, permiso-conducir, formacion-vial, carnet-moto. Estilo: vivo. Plan mínimo: gratis.
- Secciones: hero, permisos, packs, proceso, horario, flota, resultados, opiniones, preguntas, matricula, contacto (más el diseño `texto` para apartados nuevos).
- A ancho completo: bandas de borde a borde en amarillo señal, azul noche, asfalto y blanco roto; portada con foto a sangre y disco de precio; permisos en rejilla vial; packs como carriles; carretera de borde a borde con hitos; fotos a sangre 50/50; franja de flota sin márgenes; rayas viales discontinuas entre bandas; barra móvil «Llamar / WhatsApp».
- Campos propios: `permisos[]` (nombre, texto, precio, incluye, edad_minima, icono), `packs[]` (nombre, texto, precio, incluye, destacado) y `etiqueta_destacado`, `horario.horario[]` (dia, horas, clase), `flota.items[]` con foto, `resultados.items[]` (cifras), `hero.destacado` (disco de precio), `matricula.items` con formulario y desplegables de permiso y pack.
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio (`DrivingSchool`) y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos en `template.yaml`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`; fotos de la demo en `fotos.json`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) generadas para esta plantilla, sin licencias de terceros.

## Páginas propias
- Cada elemento de `secciones.permisos.permisos` con `detalle` tiene su página en `/permisos/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
