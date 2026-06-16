# 🪐 Orbital Studio — Desafío Bootstrap SASS

Proyecto final del módulo **Bootstrap 5.3 + SASS**.  
Parte de la consigna original “Pixel Studio — Agencia Digital”, adaptado a una temática propia de **planetas / espacio**.

El objetivo fue:

- Practicar las 5 mini-técnicas vistas en clase (colores, paleta, color custom, tipografía, espaciado/ decoración).
- Aplicarlas para construir una landing completa usando **Bootstrap desde SASS**, no desde CDN.

---

## 🗂 Estructura del proyecto

```text
pixel-studio/
├── index.html
├── estilos.scss          # SASS principal (override de Bootstrap)
├── scss/                 # Carpeta Bootstrap SASS (copiada del ZIP oficial)
│   ├── bootstrap.scss
│   ├── _variables.scss
│   └── ...
└── css/
    └── estilos.css       # CSS generado por Sass (no se edita a mano)
```

- `index.html`: maqueta dada por el ejercicio, luego personalizada (nombre agencia, textos, sección extra).
- `estilos.scss`: archivo que usa `@use` para importar `scss/bootstrap` y sobreescribir variables del sistema.
- `scss/`: fuente oficial de Bootstrap 5.3 (Source files).
- `css/estilos.css`: resultado de compilar `estilos.scss`.

---

## ⚙️ Cómo compilar SASS

El proyecto usa **Bootstrap desde sus fuentes SASS**, no desde CDN.

### Opción 1: CLI de Sass

Desde la carpeta `pixel-studio/`:

```bash
sass --watch estilos.scss css/estilos.css
```

Cada vez que se guarde `estilos.scss`, se regenera `css/estilos.css`.

### Opción 2: Live Sass Compiler (VS Code)

- Abrir `estilos.scss`.
- Click en “Watch Sass” en la barra inferior.
- Asegurarse de que la salida es `css/estilos.css`.

---

## 🎨 Técnicas aplicadas (5 minis → desafío)

### 1. Colores del sistema (`$primary`, `$dark`, etc.)

En `estilos.scss` se sobrescriben los colores base de Bootstrap para crear una paleta **temática espacial**:

```scss
$primary:   #2563eb;  // azul órbita
$secondary: #64748b;  // gris azulado
$success:   #22c55e;  // verde vida
$warning:   #facc15;  // amarillo estrella
$danger:    #f97373;  // rojo alerta
$dark:      #020617;  // casi negro espacio
$light:     #f8fafc;
```

Esto afecta a `.btn-primary`, `.bg-dark`, `.alert-success`, etc.

### 2. Paleta completa (`$theme-colors`)

Se configura el mapa `$theme-colors` para que todo el sistema de utilidades (bg-*, text-*, border-*) use la nueva paleta y un color extra:

```scss
$theme-colors: (
  "primary":   #2563eb,
  "secondary": #64748b,
  "success":   #22c55e,
  "info":      #0ea5e9,
  "warning":   #facc15,
  "danger":    #f97373,
  "light":     #f8fafc,
  "dark":      #020617,
  "pixel":     #7c3aed,  // barra de stats (.bg-pixel)
);
```

Clases usadas:

- `.bg-dark` en navbar y footer.
- `.btn-primary` en los CTAs.
- `.bg-pixel` en la sección de estadísticas.

### 3. Color custom en el sistema (`bg-pixel`)

El color **`"pixel"`** se añade al mapa `$theme-colors` y se usa en `index.html`:

```html
<section class="py-5 bg-pixel text-white">
  ...
</section>
```

Bootstrap genera automáticamente `.bg-pixel`, `.text-pixel`, `.border-pixel`, etc.

### 4. Tipografía (Google Fonts + variables)

En el `<head>` del `index.html` se cargan:

- **Inter** para cuerpo.
- **Plus Jakarta Sans** para headings.

En `estilos.scss` se conectan con las variables de Bootstrap:

```scss
$font-family-sans-serif: unquote('"Inter", system-ui, sans-serif');
$headings-font-family:   unquote('"Plus Jakarta Sans", "Inter", sans-serif');
$headings-font-weight:   800;
$line-height-base:       1.7;
```

Resultado:

- Body y textos generales en Inter.
- Títulos y headings en Plus Jakarta Sans.

### 5. Espaciado y decoración (spacers, radius, sombras)

Se extiende el mapa `$spacers` para incluir niveles 6 y 7:

```scss
$spacers: (
  0: 0, 1: .25rem, 2: .5rem,
  3: 1rem, 4: 1.5rem, 5: 3rem,
  6: 4rem,  // .py-6
  7: 6rem,  // .py-7
);
```

Esto permite usar `.py-6` y `.py-7` en secciones grandes (hero, bloques principales).

Se personalizan también bordes y sombras:

```scss
$border-radius:    1rem;
$border-radius-lg: 1.5rem;

$box-shadow-sm: #{0 0.25rem 0.75rem rgba(15, 23, 42, .25)};
$box-shadow:    #{0 1rem 2.5rem rgba(15, 23, 42, .35)};
$box-shadow-lg: #{0 2rem 4rem rgba(15, 23, 42, .45)};
```

Lo usan principalmente:

- `.card.shadow` en la sección de servicios.
- Cualquier componente con utilidades `.shadow`, `.shadow-lg`.

---

## 🪐 Personalización temática (planetas)

Además del brief original, se personalizaron:

- **Nombre de agencia**: de “Pixel Studio” a algo tipo `Orbital Studio` (puede variar).
- **Hero**:
  - Badge y títulos adaptados a “agencia de diseño galáctico”.
  - CTA adaptados (“Ver galaxia de proyectos”, etc.).

### Sección nueva: Planetas destacados

Se añadió una sección extra con planetas ficticios:

```html
<section class="py-6 bg-dark text-white">
  <div class="container">
    <div class="text-center mb-5">
      <h2>Planetas destacados</h2>
      <p class="text-white-50">Algunos mundos con los que ya trabajamos</p>
    </div>
    <div class="row g-4">
      <!-- planet cards -->
    </div>
  </div>
</section>
```

### Clases custom

Al final de `estilos.scss` se definieron clases propias:

```scss
.hero-stars {
  background-image: radial-gradient(circle at top, rgba(148, 163, 184, 0.4), transparent 55%);
}

.planet-card {
  background: radial-gradient(circle at top left, rgba(94, 234, 212, 0.08), transparent 55%);
}
```

Se usan para dar un look “estelar” al hero y a las cards.

---

## ✅ Checklist (ejercicio)

- [x] Carpeta `pixel-studio/` con `index.html`, `estilos.scss` y carpeta `scss/` de Bootstrap.
- [x] Colores configurados vía SASS, incluyendo color custom `"pixel"` en `$theme-colors`.
- [x] Google Fonts conectadas tanto en HTML como en las variables Sass.
- [x] `$spacers` extendido con niveles 6 y 7 (`.py-6`, `.py-7`).
- [x] Bordes y sombras personalizados para cards y componentes.
- [x] Página personalizada (nombre agencia, temática de planetas, sección nueva, clases propias).

---

**Puedes ver el resultado de este ejercicio en:**
https://zakkdruzer.github.io/orbital-studio/
