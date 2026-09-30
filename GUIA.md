# muzic: guía en español para productores

muzic es un plugin de Claude Code que **escucha un tema** y te devuelve lo que necesitás para trabajarlo en el estudio: tempo, tonalidad, acordes compás a compás, curva de energía, mood, género, rango de la melodía y loudness. Con `replicate` va un paso más allá: **reconstruye el esqueleto del tema en MIDI** para llevarlo a Ableton Live.

> muzic lo creó [Alex Gabay](https://github.com/JinKazamaMishima/muzic-plugin). Yo soy su primer usuario y tester, y esta guía es mi aporte para productores que hablan español.

## Qué necesitás

- **Claude Code**, en la terminal o en la app de escritorio de Claude.
- **Node 18 o más nuevo**. El plugin es un cliente liviano y no necesita nada más.
- La **contraseña del servicio de análisis**: el análisis corre en un servidor, no en tu compu.
- Para armar el tema en Live: **Ableton Live** conectado a Claude Code con **SMYLZ Producer**.
- Opcional: **ffmpeg**, para achicar bounces de más de 50 MB antes de subirlos.

## Instalación

En la Terminal (sirve tanto para Claude Code en la terminal como para la app de escritorio):

```bash
claude plugin marketplace add https://github.com/JinKazamaMishima/muzic-plugin.git
claude plugin install muzic@muzic
```

Reiniciá Claude y escribí en el chat:

```
/muzic:setup
```

Te pide la contraseña una vez, la guarda en `~/.muzic.json` y prueba la conexión.

## Los dos comandos

### `/muzic:listen`: describir un tema

```
/muzic:listen ~/Music/bounces/mi-tema.wav
```

En segundos te dice:

- **Tempo y tonalidad**, para mezclar en armonía o elegir samples en la misma escala.
- **Acordes compás a compás**, en una grilla de 4/4.
- **Curva de energía**: dónde sube, dónde cae, cómo está armado el drop.
- **Mood, género, rango de la melodía y loudness**.

También podés escribirle a Claude "escuchá este tema" con la ruta del archivo.

### `/muzic:replicate`: reconstruir el esqueleto

```
/muzic:replicate ~/Music/refs/tema-de-referencia.wav
```

Tarda unos minutos, casi todo en separar los stems. Cuando termina, guarda todo en `~/Music/muzic/<tema>/`:

- **Batería en MIDI con el swing** del original, más un **loop de un compás**.
- **Bajo y melodía en MIDI**.
- **Acordes y secciones** (intro, build, drop…).
- **Pistas de sonido**: qué tipo de sonidos usar para acercarte.

Con SMYLZ Producer conectado, Claude lo arma en Live **solo cuando le decís que sí**, y nunca encima de un arreglo tuyo sin preguntarte.

## Ideas para usarlo en el estudio

1. **Estudiar una referencia.** Pasale a `replicate` un tema que te guste y mirá cómo está armado: el groove de la batería, la progresión, dónde entra cada sección.
2. **Arrancar un tema propio.** Usá el esqueleto como punto de partida: cambiá los sonidos, mové notas, rompé la estructura. muzic te da el esqueleto; la música la hacés vos.
3. **Chequear tu bounce.** Antes de mezclar o de mandar un tema, usá `listen` para confirmar tempo, tonalidad y curva de energía.
4. **Preparar un set.** Con la tonalidad y el tempo de cada tema podés ordenar el set para mezclar en armonía.

## Detalles y problemas comunes

- **Formatos:** mp3, wav, flac, ogg, m4a, aac y wma.
- **Tamaño:** hasta 50 MB por archivo. Si tenés `ffmpeg`, el plugin convierte los bounces más grandes a un mp3 mono antes de subirlos.
- **Compás:** muzic asume 4/4. Si tu tema está en otro compás, avisale a Claude.
- **Live no carga los audios:** SMYLZ Producer solo lee WAVs de carpetas aprobadas. Agregá `~/Music/muzic` en el panel de SMYLZ una vez.
- **Batería en General MIDI:** bombo 36, caja 38, hi-hat cerrado 42. Si tu Drum Rack usa otro mapeo, reasigná las notas.
- **¿Anda la conexión?** Pedile a Claude que corra `muzic_health`: te dice si el servicio responde y si la contraseña es correcta.

## Créditos

muzic: [Alex Gabay](https://github.com/JinKazamaMishima/muzic-plugin). Guía en español: [Salvador Romanelli](https://salvaromanelli.github.io).
