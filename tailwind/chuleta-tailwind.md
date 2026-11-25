# Chuleta de Tailwind CSS

## Índice

- [Chuleta de Tailwind CSS](#chuleta-de-tailwind-css)
  - [Índice](#índice)
  - [Versión y compatibilidad](#versión-y-compatibilidad)
  - [Escalas y combinación de clases](#escalas-y-combinación-de-clases)
  - [Instalación y uso básico](#instalación-y-uso-básico)
  - [Flexbox](#flexbox)
  - [Grid](#grid)
  - [Margin, padding y gap](#margin-padding-y-gap)
  - [Anchura y altura](#anchura-y-altura)
  - [Tipografía y alineación de texto](#tipografía-y-alineación-de-texto)
  - [Colores y fondos](#colores-y-fondos)
  - [Bordes y esquinas redondeadas](#bordes-y-esquinas-redondeadas)
  - [Posicionamiento](#posicionamiento)
  - [Alineación y distribución de elementos](#alineación-y-distribución-de-elementos)
  - [Diseño responsive y breakpoints](#diseño-responsive-y-breakpoints)
  - [Visibilidad y display](#visibilidad-y-display)
  - [Imágenes y object-fit](#imágenes-y-object-fit)
  - [Sombras y opacidad](#sombras-y-opacidad)
  - [Hover, focus y otros estados](#hover-focus-y-otros-estados)
  - [Valores personalizados](#valores-personalizados)
  - [Documentación oficial](#documentación-oficial)

## Versión y compatibilidad

En v4 cambiaron algunos nombres y escalas: `shadow` de v3 corresponde a `shadow-sm` de v4; `rounded` de v3, a `rounded-sm` de v4. Para evitar dudas, aquí se usan sobre todo tamaños explícitos como `shadow-md`, `rounded-lg` y `ring-2`. [Diferencias oficiales entre v3 y v4](https://tailwindcss.com/docs/upgrade-guide).

## Escalas y combinación de clases

Con el tema predeterminado, el espaciado sigue la fórmula **número × 0.25rem**. Si `1rem = 16px`, cada unidad equivale a 4px. Se aplica a `p-*`, `m-*`, `gap-*`, `w-*` y `h-*`, entre otras. Personalizar el tema puede cambiar esos valores.

| Clase o sintaxis | Qué hace | Ejemplo |
| ---------------- | -------- | ------- |
| `p-0`, `p-1`, `p-2` | Padding de 0, 4 y 8px. | `class="p-2"` |
| `p-3`, `p-4`, `p-6`, `p-8` | Padding de 12, 16, 24 y 32px. | `class="p-6"` |
| `p-0.5`, `p-1.5` | Medias unidades: 2 y 6px. | `class="p-1.5"` |
| `w-12`, `h-12` | Dimensiones de 3rem: normalmente 48px. | `class="w-12 h-12"` |
| `p-px` | Un píxel exacto, sin multiplicar por 4. | `class="p-px"` |
| `border-2` | El número indica píxeles de borde. | Borde de 2px. |
| `grid-cols-3` | El número indica cantidad de columnas. | Tres columnas iguales. |
| `text-2xl`, `bg-blue-700` | Tamaño tipográfico y tono de color; no usan la escala de espaciado. | Título grande y fondo azul oscuro. |

Las clases se separan con espacios y sus efectos se combinan:

```html
<button class="rounded-lg bg-blue-700 px-6 py-3 font-bold text-white hover:bg-blue-800">
    Guardar
</button>
```

Evita clases que compitan en la misma condición, como `p-4 p-8`: **el orden en el atributo `class` no decide cuál gana**; lo decide el CSS generado. Sí tiene sentido `p-4 md:p-8`, porque cambia según la anchura.

## Instalación y uso básico

Los comandos son ejemplos de consulta; no hay que ejecutarlos para leer esta guía. La CLI genera el CSS a partir de las clases que encuentra en los archivos.

| Clase o sintaxis | Qué hace | Ejemplo |
| ---------------- | -------- | ------- |
| `npm ci` | Instala las dependencias fijadas en el lockfile existente. | Ejecutar desde `tailwind/`. |
| `npm install tailwindcss@4.3.5 @tailwindcss/cli@4.3.5` | Instala Tailwind y su CLI en un proyecto nuevo con esta versión. | Ejecutar en la carpeta del proyecto nuevo. |
| `@import "tailwindcss";` | Importa Tailwind en el CSS de entrada de v4. | Dentro de `src/input.css`. |
| `npx @tailwindcss/cli -i ./src/input.css -o ./src/output.css --watch` | Compila y actualiza el CSS al guardar. | Desde la carpeta que contiene `src/`. |
| `<link rel="stylesheet" href="./src/output.css">` | Carga el CSS compilado. | Dentro del `<head>`. |
| `<meta name="viewport" content="width=device-width, initial-scale=1.0">` | Permite que el responsive use la anchura del dispositivo. | Dentro del `<head>`. |
| `class="..."` | Aplica utilidades al elemento. | `<h1 class="text-3xl font-bold">Título</h1>` |
| CDN v4: `https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4` | Prueba Tailwind sin compilar; pensado para desarrollo. | `<script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>` |
| CDN v3: `https://cdn.tailwindcss.com` | Método que utiliza actualmente Biciclo. | `<script src="https://cdn.tailwindcss.com"></script>` |


```sh
npx @tailwindcss/cli -i ./ejercicioCafeAroma/src/input.css -o ./ejercicioCafeAroma/src/output.css --watch
```

El script `npm run play` del proyecto usa `./src/`: sus rutas presuponen otra ubicación de esos archivos. Usa rutas que existan. En v4 no se necesita `npx tailwindcss init` para este montaje básico.

## Flexbox

Las clases de dirección y reparto necesitan un contenedor `flex`. `flex-1`, `grow` y `shrink-0` se aplican a sus hijos.

| Clase o sintaxis | Qué hace | Ejemplo |
| ---------------- | -------- | ------- |
| `flex` | Activa Flexbox. | `class="flex gap-4"` |
| `flex-row`, `flex-col` | Coloca los hijos en fila o columna. | `class="flex flex-col"` |
| `flex-row-reverse`, `flex-col-reverse` | Invierte el sentido visual. | `class="flex flex-row-reverse"` |
| `flex-wrap` | Permite saltar a otra línea. | `class="flex flex-wrap gap-4"` |
| `flex-nowrap` | Mantiene una sola línea; no garantiza que todo quepa. | `class="flex flex-nowrap"` |
| `flex-1` | Permite al hijo crecer y encogerse, sin partir de su tamaño inicial. | `class="flex-1"` |
| `flex-none` | Evita que el hijo crezca o se encoja. | `class="w-24 flex-none"` |
| `grow`, `grow-0` | Permite o impide crecer. | `class="grow"` |
| `shrink-0` | Evita que el hijo se estreche. | Icono con `class="w-6 shrink-0"`. |
| `order-1`, `order-2` | Cambia el orden visual de los hijos. | `class="order-2"` |

## Grid

| Clase o sintaxis | Qué hace | Ejemplo |
| ---------------- | -------- | ------- |
| `grid` | Activa Grid. | `class="grid gap-6"` |
| `grid-cols-1`, `grid-cols-2`, `grid-cols-3`, `grid-cols-4` | Crea columnas de igual anchura. | `class="grid grid-cols-3"` |
| `grid-rows-2` | Define dos filas de igual tamaño. | `class="grid grid-rows-2"` |
| `col-span-2` | El hijo ocupa dos columnas. | `class="col-span-2"` |
| `col-span-full` | El hijo ocupa todas las columnas. | Cabecera con `class="col-span-full"`. |
| `row-span-2` | El hijo ocupa dos filas. | `class="row-span-2"` |
| `col-start-2` | Sitúa el hijo desde la segunda línea de columna. | `class="col-start-2"` |
| `auto-rows-fr` | Da el mismo tamaño a las filas creadas automáticamente. | `class="grid auto-rows-fr"` |

```html
<div class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-3">
    <article class="rounded-xl border border-slate-200 p-6">Servicio 1</article>
    <article class="rounded-xl border border-slate-200 p-6">Servicio 2</article>
    <article class="rounded-xl border border-slate-200 p-6">Servicio 3</article>
</div>
```

## Margin, padding y gap

`m` separa por fuera; `p`, por dentro. `gap` separa hijos de un contenedor flex o grid.

| Clase o sintaxis | Qué hace | Ejemplo |
| ---------------- | -------- | ------- |
| `m-4`, `p-4` | Espacio en los cuatro lados. | `class="m-4 p-4"` |
| `mx-4`, `my-4` | Margen horizontal o vertical en escritura habitual. | `class="mx-4 my-8"` |
| `px-6`, `py-3` | Padding horizontal o vertical. | `class="px-6 py-3"` |
| `mt-4`, `mr-4`, `mb-4`, `ml-4` | Margen arriba, derecha, abajo o izquierda. | `class="mt-6 mb-4"` |
| `pt-4`, `pr-4`, `pb-4`, `pl-4` | Padding de un lado concreto. | `class="pl-8"` |
| `mx-auto` | Centra horizontalmente un bloque con anchura limitada. | `class="mx-auto max-w-6xl"` |
| `ml-auto` | Usa el margen izquierdo disponible; útil en una fila flex. | Enlace final con `class="ml-auto"`. |
| `-mt-2` | Margen superior negativo. | `class="-mt-2"` |
| `gap-4` | Separa filas y columnas. | `class="grid gap-4"` |
| `gap-x-6`, `gap-y-3` | Separa columnas y filas por separado. | `class="flex flex-wrap gap-x-6 gap-y-3"` |
| `space-y-4` | Añade separación vertical entre hermanos. | `class="flex flex-col space-y-4"` |

Usa preferentemente `gap` en flex y grid; no añadas también márgenes para conseguir la misma separación.

## Anchura y altura

| Clase o sintaxis | Qué hace | Ejemplo |
| ---------------- | -------- | ------- |
| `w-24`, `h-16` | Anchura y altura según la escala. | `class="w-24 h-16"` |
| `w-full`, `h-full` | Ocupa el 100% de la dimensión del contenedor. | Campo con `class="w-full"`. |
| `w-1/2`, `w-1/3`, `w-2/3` | Anchura proporcional al contenedor. | `class="w-1/2"` |
| `w-auto`, `h-auto` | Deja que el navegador calcule la dimensión. | Imagen con `class="w-full h-auto"`. |
| `w-screen`, `h-screen` | Anchura de 100vw y altura de 100vh. | `class="h-screen"` |
| `min-h-screen` | Altura mínima de una pantalla; permite crecer. | `class="min-h-screen"` |
| `h-dvh` | Altura de la ventana visible, adaptada a barras móviles. | `class="h-dvh"` |
| `min-w-0` | Permite reducir un hijo flex o grid por debajo de su contenido. | `class="min-w-0 flex-1"` |
| `max-w-sm`, `max-w-xl`, `max-w-6xl` | Limita la anchura a 24, 36 o 72rem. | `class="mx-auto w-full max-w-6xl"` |
| `max-w-full`, `max-h-64` | Limita la anchura al padre o la altura a 16rem. | `class="max-w-full max-h-64"` |

`h-full` necesita que la altura del contenedor esté definida. Para secciones con texto suele convenir `min-h-*` en vez de una altura fija. En una página normal, `w-full` suele encajar mejor que `w-screen`, que puede provocar desbordamiento por la barra de scroll.

## Tipografía y alineación de texto

Los tamaños en píxeles suponen `1rem = 16px`.

| Clase o sintaxis | Qué hace | Ejemplo |
| ---------------- | -------- | ------- |
| `font-sans`, `font-serif`, `font-mono` | Selecciona una familia de fuentes estándar. | `class="font-sans"` |
| `text-xs`, `text-sm`, `text-base` | Tamaño de 12, 14 o 16px. | `class="text-sm"` |
| `text-lg`, `text-xl`, `text-2xl` | Tamaño de 18, 20 o 24px. | `class="text-xl"` |
| `text-3xl`, `text-4xl`, `text-5xl` | Tamaño de 30, 36 o 48px. | `class="text-4xl"` |
| `font-normal`, `font-medium`, `font-semibold`, `font-bold` | Peso de 400, 500, 600 o 700. | `class="font-bold"` |
| `text-left`, `text-center`, `text-right`, `text-justify` | Alinea el texto dentro del elemento. | `class="text-center"` |
| `leading-6`, `leading-8` | Altura de línea de 1.5 o 2rem. | `class="text-base leading-6"` |
| `leading-tight`, `leading-relaxed` | Interlineado proporcional de 1.25 o 1.625. | `class="leading-relaxed"` |
| `tracking-tight`, `tracking-wide` | Reduce o amplía el espacio entre letras. | `class="tracking-wide"` |
| `uppercase`, `lowercase`, `capitalize` | Cambia la presentación de mayúsculas. | `class="uppercase"` |
| `italic`, `not-italic` | Activa o elimina la cursiva. | `class="italic"` |
| `underline`, `no-underline`, `line-through` | Subrayado, sin subrayado o tachado. | Precio anterior con `class="line-through"`. |
| `truncate` | Recorta a una línea con puntos suspensivos; necesita anchura limitada. | `class="block w-48 truncate"` |

`text-center` centra texto; para centrar cajas usa las utilidades de alineación de elementos.

## Colores y fondos

Formato habitual: `propiedad-familia-tono`. En las paletas, `50` suele ser muy claro y `950` muy oscuro; el número no indica píxeles ni opacidad.

| Clase o sintaxis | Qué hace | Ejemplo |
| ---------------- | -------- | ------- |
| `text-slate-900`, `text-slate-600` | Texto oscuro o secundario. | `class="text-slate-600"` |
| `text-white`, `text-black` | Texto blanco o negro. | `class="text-white"` |
| `bg-white`, `bg-slate-100` | Fondo blanco o gris claro. | `class="bg-slate-100"` |
| `bg-blue-700`, `bg-yellow-300` | Fondo azul o amarillo. | `class="bg-blue-700 text-white"` |
| `bg-transparent` | Fondo transparente. | `class="bg-transparent"` |
| `bg-blue-700/50` | Fondo azul con un 50% de opacidad. | El texto conserva su opacidad. |
| `bg-cover`, `bg-contain` | Ajusta una imagen de fondo cubriendo o encajando. | `class="bg-cover"` |
| `bg-center`, `bg-no-repeat` | Centra el fondo y evita que se repita. | `class="bg-center bg-no-repeat"` |
| `bg-[url('./assets/taller.svg')]` | Usa una imagen como fondo. | Combinar con `bg-cover bg-center`. |

Familias frecuentes: `slate`, `gray`, `red`, `orange`, `yellow`, `green`, `blue`, `indigo` y `purple`.

## Bordes y esquinas redondeadas

| Clase o sintaxis | Qué hace | Ejemplo |
| ---------------- | -------- | ------- |
| `border`, `border-2`, `border-4` | Borde de 1, 2 o 4px. | `class="border border-slate-200"` |
| `border-0` | Elimina el ancho del borde. | `class="border-0"` |
| `border-t`, `border-r`, `border-b`, `border-l` | Borde de 1px en un lado. | `class="border-b border-slate-200"` |
| `border-blue-700`, `border-slate-300` | Define el color del borde. | `class="border-2 border-blue-700"` |
| `border-solid`, `border-dashed`, `border-dotted` | Define el estilo del borde. | `class="border-2 border-dashed"` |
| `rounded-none` | Esquinas rectas. | `class="rounded-none"` |
| `rounded-md`, `rounded-lg`, `rounded-xl` | Radio de 6, 8 o 12px. | `class="rounded-lg"` |
| `rounded-2xl`, `rounded-3xl` | Radio de 16 o 24px. | Tarjeta con `class="rounded-2xl"`. |
| `rounded-full` | Redondeo máximo; círculo si ancho y alto son iguales. | `class="w-12 h-12 rounded-full"` |
| `rounded-t-lg`, `rounded-b-lg` | Redondea solo las esquinas superiores o inferiores. | `class="rounded-t-lg"` |

Define el color del borde explícitamente: su valor predeterminado cambió entre v3 y v4.

## Posicionamiento

| Clase o sintaxis | Qué hace | Ejemplo |
| ---------------- | -------- | ------- |
| `static` | Posición normal del documento. | `class="static"` |
| `relative` | Mantiene su espacio y sirve de referencia a hijos absolutos. | Contenedor con `class="relative"`. |
| `absolute` | Sale del flujo y se sitúa respecto al ancestro posicionado más cercano. | `class="absolute top-2 right-2"` |
| `fixed` | Sale del flujo y normalmente se fija a la ventana. | `class="fixed bottom-4 right-4"` |
| `sticky top-0` | Se pega al borde superior al hacer scroll dentro de su contenedor. | `class="sticky top-0"` |
| `top-4`, `right-0`, `bottom-4`, `left-0` | Desplazamiento desde cada lado. | `class="absolute top-4 left-0"` |
| `inset-0` | Sitúa los cuatro lados en cero. | Capa con `class="absolute inset-0"`. |
| `z-10`, `z-20`, `z-50` | Orden de superposición dentro del contexto de apilamiento. | Cabecera con `class="sticky top-0 z-10"`. |
| `scroll-mt-24` | Reserva margen al navegar a un ancla, útil con cabecera fija. | `<section id="contacto" class="scroll-mt-24">` |

Para `sticky`, define un límite como `top-0`; revisa también el scroll y el `overflow` de los contenedores padres.

## Alineación y distribución de elementos

En `flex-row`, el eje principal es horizontal; en `flex-col`, vertical. `justify-*` reparte en el eje principal y `items-*` alinea en el transversal.

| Clase o sintaxis | Qué hace | Ejemplo |
| ---------------- | -------- | ------- |
| `justify-start`, `justify-center`, `justify-end` | Agrupa al inicio, centro o final del eje principal. | `class="flex justify-center"` |
| `justify-between` | Deja espacio entre hijos, sin espacio extra en los extremos. | `class="flex justify-between"` |
| `justify-around` | Deja espacio alrededor de cada hijo; menos en los extremos. | `class="flex justify-around"` |
| `justify-evenly` | Deja el mismo espacio entre hijos y extremos. | `class="flex justify-evenly"` |
| `items-start`, `items-center`, `items-end` | Alinea los hijos en el eje transversal. | `class="flex items-center"` |
| `items-stretch` | Estira los hijos en el eje transversal si su tamaño lo permite. | `class="flex items-stretch"` |
| `self-center`, `self-end`, `self-stretch` | Cambia la alineación de un único hijo. | Hijo con `class="self-end"`. |
| `content-center`, `content-between` | Distribuye líneas flex o filas grid cuando sobra espacio transversal. | `class="flex h-64 flex-wrap content-between"` |
| `justify-items-center` | Centra horizontalmente los hijos dentro de sus celdas grid. | `class="grid justify-items-center"` |
| `place-items-center` | Centra los hijos en ambos ejes de sus celdas grid. | `class="grid h-64 place-items-center"` |

```html
<header class="flex items-center justify-between gap-4 p-4">
    <span class="font-bold">Mi web</span>
    <nav class="flex gap-4">
        <a href="#inicio">Inicio</a>
        <a href="#contacto">Contacto</a>
    </nav>
</header>
```

## Diseño responsive y breakpoints

Se escribe `prefijo:clase`, sin espacios alrededor de `:`. Las clases sin prefijo se aplican a cualquier anchura; las prefijadas actúan **desde el mínimo indicado hacia arriba**. `sm:` no significa «solo móvil».

| Clase o sintaxis | Qué hace | Ejemplo |
| ---------------- | -------- | ------- |
| Sin prefijo | Estilo base, también en pantallas pequeñas. | `class="grid-cols-1"` |
| `sm:` | Desde 40rem, normalmente 640px. | `sm:grid-cols-2` |
| `md:` | Desde 48rem, normalmente 768px. | `md:flex-row` |
| `lg:` | Desde 64rem, normalmente 1024px. | `lg:grid-cols-3` |
| `xl:` | Desde 80rem, normalmente 1280px. | `xl:px-12` |
| `2xl:` | Desde 96rem, normalmente 1536px. | `2xl:max-w-7xl` |
| `max-md:` | Por debajo de 48rem. | `max-md:hidden` |
| `md:max-lg:` | Desde 48rem hasta antes de 64rem. | `md:max-lg:grid-cols-2` |
| `md:hover:` | Combina anchura y estado. | `md:hover:bg-blue-800` |

`grid-cols-1 sm:grid-cols-2 lg:grid-cols-3` muestra una columna por defecto, dos desde 640px y tres desde 1024px. Los valores indicados son los predeterminados; un tema puede cambiarlos.

## Visibilidad y display

| Clase o sintaxis | Qué hace | Ejemplo |
| ---------------- | -------- | ------- |
| `block` | Muestra como bloque. | Etiqueta con `class="block"`. |
| `inline` | Muestra dentro de la línea de texto. | `class="inline"` |
| `inline-block` | Sigue en línea y admite ancho, alto y padding. | Enlace con `class="inline-block px-4 py-2"`. |
| `inline-flex` | Contenedor flex que participa en línea. | `class="inline-flex items-center gap-2"` |
| `hidden` | Oculta y no reserva espacio. | `class="hidden md:block"` |
| `invisible` | Oculta visualmente y mantiene el espacio. | `class="invisible"` |
| `visible` | Restaura la visibilidad. | `class="invisible md:visible"` |
| `sr-only` | Oculta visualmente, conservando el contenido para lectores de pantalla. | Texto auxiliar con `class="sr-only"`. |
| `overflow-hidden` | Recorta el contenido que sobresale. | `class="overflow-hidden rounded-xl"` |
| `overflow-auto`, `overflow-x-auto` | Añade scroll si hace falta, general u horizontal. | Tabla dentro de `class="overflow-x-auto"`. |

## Imágenes y object-fit

| Clase o sintaxis | Qué hace | Ejemplo |
| ---------------- | -------- | ------- |
| `w-full h-auto` | Ajusta el ancho conservando la proporción natural. | `class="w-full h-auto"` |
| `object-cover` | Llena la caja sin deformar; puede recortar. | `class="w-full h-48 object-cover"` |
| `object-contain` | Muestra la imagen completa sin deformar; puede dejar huecos. | `class="w-full h-48 object-contain"` |
| `object-fill` | Llena la caja y puede deformar la imagen. | `class="w-64 h-48 object-fill"` |
| `object-none` | Conserva el tamaño natural del contenido. | `class="w-64 h-48 object-none"` |
| `object-center`, `object-top` | Coloca la imagen dentro de su caja. | `class="object-cover object-top"` |
| `aspect-square` | Caja con proporción 1:1. | `class="w-full aspect-square object-cover"` |
| `aspect-video` | Caja con proporción 16:9. | `class="w-full aspect-video object-cover"` |

`object-*` ajusta el contenido de un `<img>`; `bg-*` ajusta fondos. Para apreciar `object-fit`, la caja debe tener dimensiones o una proporción definidas.

## Sombras y opacidad

| Clase o sintaxis | Qué hace | Ejemplo |
| ---------------- | -------- | ------- |
| `shadow-sm` | Sombra pequeña; su aspecto cambia entre v3 y v4. | `class="shadow-sm"` |
| `shadow-md`, `shadow-lg`, `shadow-xl` | Sombras de intensidad creciente. | Tarjeta con `class="shadow-md"`. |
| `shadow-none` | Elimina la sombra. | `class="shadow-none"` |
| `shadow-blue-500/30` | Colorea una sombra con opacidad del 30%. | `class="shadow-lg shadow-blue-500/30"` |
| `opacity-100`, `opacity-75`, `opacity-50`, `opacity-0` | Opacidad del elemento completo, incluidos sus hijos. | `class="opacity-50"` |
| `bg-black/50` | Solo el color de fondo es semitransparente. | Capa con `class="bg-black/50"`. |

`opacity-0` mantiene el espacio y puede seguir recibiendo clics; no equivale a `hidden`.

## Hover, focus y otros estados

Un prefijo aplica una utilidad solo cuando se cumple su condición. No necesita una transición para funcionar. En v4, `hover:` se limita a dispositivos que permiten pasar el puntero.

| Clase o sintaxis | Qué hace | Ejemplo |
| ---------------- | -------- | ------- |
| `hover:` | Al pasar el puntero. | `hover:bg-blue-800` |
| `focus:` | Cuando el elemento tiene el foco. | `focus:border-blue-700` |
| `focus-visible:` | Cuando el navegador considera necesario mostrar el foco, normalmente al usar teclado. | `focus-visible:ring-2 focus-visible:ring-blue-700` |
| `active:` | Mientras se pulsa. | `active:bg-blue-900` |
| `disabled:` | Cuando un control está deshabilitado. | `disabled:opacity-50` |
| `checked:` | Cuando un checkbox o radio está marcado. | `checked:accent-blue-700` |
| `invalid:` | Cuando un campo no cumple la validación HTML. | `invalid:border-red-500` |
| `first:`, `last:`, `odd:`, `even:` | Según la posición entre hermanos. | Filas con `even:bg-slate-100`. |
| `group` + `group-hover:` | El hijo reacciona al hover de un padre marcado. | Padre `group`; hijo `group-hover:text-blue-700`. |
| `peer` + `peer-checked:` | Un hermano posterior reacciona al checkbox marcado. | Checkbox `peer`; menú `hidden peer-checked:flex`. |

```html
<input id="menu" type="checkbox" class="peer sr-only">
<label for="menu" class="inline-block rounded-lg border p-2">Abrir o cerrar menú</label>
<nav class="hidden flex-col gap-2 p-4 peer-checked:flex">
    <a href="#servicios" class="hover:text-blue-700">Servicios</a>
</nav>
```

El elemento `peer` debe aparecer **antes** del elemento que reacciona, y ambos deben compartir padre. Conserva una indicación visible del foco para quien navega con teclado.

## Valores personalizados

Úsalos cuando la escala no resuelva una necesidad concreta. Escribe las clases completas para que Tailwind pueda detectarlas al compilar.

| Clase o sintaxis | Qué hace | Ejemplo |
| ---------------- | -------- | ------- |
| `w-[300px]` | Anchura exacta. | `class="w-[300px] max-w-full"` |
| `min-h-[50vh]` | Altura mínima de media ventana. | `class="min-h-[50vh]"` |
| `text-[18px]` | Tamaño de fuente exacto. | `class="text-[18px]"` |
| `bg-[#123456]` | Color hexadecimal personalizado. | `class="bg-[#123456]"` |
| `grid-cols-[1fr_2fr]` | Dos columnas, la segunda con el doble de espacio flexible. | `class="grid grid-cols-[1fr_2fr]"` |
| `w-[calc(100%-2rem)]` | Anchura calculada. | `class="w-[calc(100%-2rem)]"` |
| `bg-[var(--marca)]` | Usa una variable CSS definida previamente. | `style="--marca: #123456" class="bg-[var(--marca)]"` |
| `bg-(--marca)` | Abreviatura de la fila anterior, exclusiva de v4. | `class="bg-(--marca)"` |
| `@theme { --color-marca: #123456; }` | Define un color reutilizable en el CSS de entrada, en v4. | Después se puede usar `bg-marca` o `text-marca`. |

Dentro de valores entre corchetes, `_` representa normalmente un espacio. No escribas `grid-cols-[1fr 2fr]`, porque el HTML lo separaría en dos clases. `@theme` es sintaxis de v4; en v3 se configura el tema de otra forma.

## Documentación oficial

Consulta realizada el 25 de noviembre de 2026. Valores y ejemplos referidos al tema predeterminado.

- [Instalación con CLI, v4](https://tailwindcss.com/docs/installation/tailwind-cli), [CDN v4](https://tailwindcss.com/docs/installation/play-cdn) y [CDN v3](https://v3.tailwindcss.com/docs/installation/play-cdn).
- [Uso de clases y resolución de conflictos](https://tailwindcss.com/docs/styling-with-utility-classes) y [migración de v3 a v4](https://tailwindcss.com/docs/upgrade-guide).
- Flexbox: [flex](https://tailwindcss.com/docs/flex), [dirección](https://tailwindcss.com/docs/flex-direction) y [salto de línea](https://tailwindcss.com/docs/flex-wrap).
- Grid: [columnas](https://tailwindcss.com/docs/grid-template-columns), [ocupación de columnas](https://tailwindcss.com/docs/grid-column) y [filas](https://tailwindcss.com/docs/grid-template-rows).
- Espaciado: [margin](https://tailwindcss.com/docs/margin), [padding](https://tailwindcss.com/docs/padding) y [gap](https://tailwindcss.com/docs/gap).
- Tamaños: [anchura](https://tailwindcss.com/docs/width), [altura](https://tailwindcss.com/docs/height) y [anchura máxima](https://tailwindcss.com/docs/max-width).
- Texto: [tamaño](https://tailwindcss.com/docs/font-size), [peso](https://tailwindcss.com/docs/font-weight), [interlineado](https://tailwindcss.com/docs/line-height) y [alineación](https://tailwindcss.com/docs/text-align).
- Colores: [paleta](https://tailwindcss.com/docs/colors), [fondos](https://tailwindcss.com/docs/background-color) y [tamaño del fondo](https://tailwindcss.com/docs/background-size).
- Bordes: [grosor](https://tailwindcss.com/docs/border-width) y [esquinas redondeadas](https://tailwindcss.com/docs/border-radius).
- Posición: [position](https://tailwindcss.com/docs/position), [desplazamientos](https://tailwindcss.com/docs/top-right-bottom-left) y [z-index](https://tailwindcss.com/docs/z-index).
- Alineación: [justify-content](https://tailwindcss.com/docs/justify-content), [align-items](https://tailwindcss.com/docs/align-items), [align-self](https://tailwindcss.com/docs/align-self) y [place-items](https://tailwindcss.com/docs/place-items).
- [Responsive y breakpoints](https://tailwindcss.com/docs/responsive-design).
- Visibilidad: [display](https://tailwindcss.com/docs/display), [visibility](https://tailwindcss.com/docs/visibility) y [overflow](https://tailwindcss.com/docs/overflow).
- Imágenes: [object-fit](https://tailwindcss.com/docs/object-fit), [object-position](https://tailwindcss.com/docs/object-position) y [aspect-ratio](https://tailwindcss.com/docs/aspect-ratio).
- Efectos: [sombras](https://tailwindcss.com/docs/box-shadow) y [opacidad](https://tailwindcss.com/docs/opacity).
- [Hover, focus y otros estados](https://tailwindcss.com/docs/hover-focus-and-other-states).
- [Valores personalizados](https://tailwindcss.com/docs/adding-custom-styles), [variables del tema](https://tailwindcss.com/docs/theme) y [detección de clases](https://tailwindcss.com/docs/detecting-classes-in-source-files).
