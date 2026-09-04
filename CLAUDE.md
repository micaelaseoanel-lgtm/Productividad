# Mi Productividad

PWA de organización de tareas (personal + laboral) para Micaela. Un solo archivo `index.html` con
HTML/CSS/JS vanilla (sin build — todo corre directo en el navegador, sin framework ni bundler).
El estado se sincroniza entre dispositivos vía Firebase (Auth con Google + Firestore), con
`localStorage` como caché local, y registro de service worker (`sw.js`) para uso offline con `manifest.json`.

Repo: `https://github.com/micaelaseoanel-lgtm/Productividad` (público, para permitir GitHub Pages
gratis). Publicado en `https://micaelaseoanel-lgtm.github.io/Productividad/`.

## Alcance actual (no tocar sin que se pida explícitamente)

- **Sin build step, pero con backend gestionado (Firebase).** Todo el código sigue viviendo en
  `index.html` (un solo `<script>` con render manual del DOM vía `innerHTML`, sin framework). Firebase
  se agrega vía SDK "compat" por `<script src="https://www.gstatic.com/firebasejs/...">` (sin npm), para
  no romper la filosofía de "sin build".
- **Auth:** Firebase Authentication, único método habilitado: **Google (signInWithRedirect)**. No hay
  login con email/contraseña implementado en el código (aunque el proveedor está habilitado en la
  consola de Firebase, no se usa).
- **Persistencia y sincronización:**
  - Fuente de verdad: Firestore, colección `users`, un documento por usuario en `users/{uid}` con
    el estado completo (`{ tasks, distractions, people }`) como un solo blob, igual forma que antes.
  - `localStorage` (clave `mica-productividad-v1`) actúa como caché local/offline, se sigue
    actualizando en cada `save()`.
  - `save()` escribe a `localStorage` y a Firestore (si hay usuario logueado). Un listener
    `onSnapshot` en `users/{uid}` es lo que empuja los cambios remotos (de otro dispositivo) al
    estado local y dispara `render()`.
  - Primer login de una cuenta nueva: si el doc de Firestore no existe, se sube lo que haya en
    `localStorage` de ese dispositivo (migración automática). Si el doc ya existe, se descarga y
    pisa el estado local (así un dispositivo nuevo se pone al día con la nube).
  - Si cambiás la forma del estado, actualizá `EMPTY_STATE` y pensá en migración de datos existentes
    (tanto en `localStorage` como en los documentos ya guardados en Firestore).
- **Config de Firebase:** proyecto `mi-productividad-c8cf2`, cuenta personal de Micaela
  (`micaela.seoane.l@gmail.com`), plan gratuito (Spark). El objeto `firebaseConfig` en el código
  (apiKey, authDomain, etc.) no es secreto — la seguridad la dan las reglas de Firestore, que
  restringen cada documento a `request.auth.uid == userId`.
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
