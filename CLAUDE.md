# Mi Productividad

PWA de organización de tareas (personal + laboral) para Micaela. Un solo archivo `index.html` con
HTML/CSS/JS vanilla (sin build, sin dependencias — todo corre directo en el navegador), estado
persistido en `localStorage`, y registro de service worker (`sw.js`) para uso offline con `manifest.json`.

## Alcance actual (no tocar sin que se pida explícitamente)

- **No hay backend ni build step.** Todo vive en `index.html` (un solo `<script>` con render manual
  del DOM vía `innerHTML`, sin framework).
- **Persistencia:** `localStorage`, clave `mica-productividad-v1`. Si cambiás la forma del estado,
  actualizá `EMPTY_STATE` y pensá en migración de datos existentes (la gente ya puede tener datos guardados).
- **Vistas (tabs):** Hoy, Calendario, Histórico, Personas.
- **Tags fijos:** `personal` y `laboral` (objeto `TAGS` en el JS), cada uno con color propio.
- **Fuera de alcance por ahora:** control de gastos / plata. Se evaluará como proyecto aparte más adelante — no mezclar acá.

## Estilo visual (mantener consistencia)

- Paleta: fondo `#ECEAE3`, texto `#22291F`, acento principal `#2F5D50` (verde), acento cálido `#A6763E`,
  rojo de alerta `#A63A3A`.
- Tipografía: `Fraunces` (serif, para títulos/headline) + `Inter` (sans, para todo el resto), vía Google Fonts.
- Tarjetas blancas redondeadas (`border-radius: 14px`), chips/pills redondeados, sin sombras duras.
- Mobile-first, pensado para PWA instalada (标准 standalone display).

## Cómo correr / probar

No requiere instalación. Para probar local:

```bash
python3 -m http.server 8000
# abrir http://localhost:8000
```

El service worker cachea `./`, `./index.html`, `./manifest.json`, `./icon-192.png`, `./icon-512.png`.
Si agregás archivos nuevos que deban estar disponibles offline, sumalos al array `ASSETS` en `sw.js`
y subí la versión de `CACHE` (ej: `mica-productividad-v2`) para forzar la actualización del cache en los
dispositivos que ya tienen la app instalada.

## Objetivo de esta sesión de trabajo

Iterar sobre la organización de tareas (personal y laboral) para que la herramienta sea lo más
eficiente y eficaz posible. Sin instrucciones puntuales todavía sobre qué cambiar — arrancar
preguntando qué se quiere mejorar o agregar antes de escribir código.
