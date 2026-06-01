# offliner

Un visor **offline y privado** de tu archivo de X (Twitter) — un baúl de recuerdos
para abrir hoy y dentro de diez años. Un solo `index.html`, sin build, sin
dependencias, sin red. Lo abrís con doble clic y listo.

> Pensado también para sumar, más adelante, tu archivo de **Facebook**. De ahí el
> nombre: lo que bajaste de las redes, para verlo *offline*.

## Por qué

El export oficial de X es un `.zip` con miles de `.js` y un visor feo y limitado.
`offliner` lo transforma en algo lindo de habitar: navegás por **épocas** (año a
año), reconstruye tus **hilos**, te muestra **stats**, **"tal día como hoy"**, tus
**likes**, y todo con filtros y búsqueda — sin que un solo byte salga de tu máquina.

## Privacidad (lo más importante)

- **100% client-side, cero red.** No hay analytics, ni telemetría, ni requests
  externos. Una CSP (`connect-src 'none'`) bloquea fetch/XHR/websockets.
- **Tus datos nunca se versionan.** La carpeta `data/` está en `.gitignore`: tu
  archivo personal se queda en tu disco, nunca en GitHub.
- Fuentes del sistema (sin CDNs). Funciona con `file://` real, sin servidor.

## Cómo usarlo

1. Descargá tu archivo de X: *Settings → Your account → Download an archive of your data*.
2. Descomprimílo. Vas a tener una carpeta tipo `twitter-2026-05-31-abc123…/`.
3. Movéla dentro de `data/` y renombrala a **`twitter`** (queda `data/twitter/`,
   con su `Your archive.html`, `assets/` y `data/` adentro).
   - Si preferís otro nombre/ubicación, cambiá la constante `EXPORT_ROOT` arriba
     de todo en `index.html`.
4. Abrí **`index.html`** con doble clic.

```
offliner/
├── index.html          ← el visor (esto es lo único que se versiona como código)
├── README.md
├── .gitignore
└── data/               ← tus archivos (ignorado por git)
    └── twitter/        ← acá va tu export de X
        ├── Your archive.html
        ├── assets/
        └── data/       ← manifest.js, tweets.js, tweets_media/, …
```

## Qué hace

- **Tweets** — timeline cronológico con **divisores de año** y una tira de épocas
  para saltar; orden ascendente/descendente; filtros por año/mes, tipo
  (propios/respuestas/RTs), con media y con ubicación; búsqueda full-text (incluye
  los dominios de los links).
- **Hilos** — reconstruye tus *self-threads* encadenando respuestas a vos mismo que
  estén dentro del archivo.
- **Tal día como hoy** — efemérides por mes-día, con selector de fecha.
- **Likes** — la lista de tus likes con su texto (los que el archivo no trae los
  marca honestamente).
- **Stats** — totales, tweets por año, top por favoritos/RTs, hashtags y menciones
  más usados.
- **Media local** — fotos, videos y gifs servidos desde tu propio archivo.
- **Permalinks** por tweet (con `Esc`/clic afuera para cerrar).

## Honestidad sobre los límites

El export sólo tiene **tu lado**. `offliner` nunca inventa lo que no está:

- Las **respuestas a terceros** muestran tu tweet y marcan que el original no está
  en el archivo (con un link "ver en X" por si querés abrirlo online).
- Los **retweets** muestran el texto tal cual (a veces recortado con `…`); el
  original no viene embebido.
- Los **quotes** enlazan al tweet citado pero avisan que no está en el archivo.

## Roadmap

- [ ] Módulo de **Facebook** (`data/facebook/`), reusando el mismo core.

## Créditos

Inspirado en la idea de [ronilaukkarinen/tweets](https://github.com/ronilaukkarinen/tweets).
El formato del export de X está documentado en `RECON.md` (local, no versionado).

Uso personal.
