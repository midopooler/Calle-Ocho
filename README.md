# Calle Ocho Sessions

A Cuban café band you can play in the browser. Click an instrument or play it from your keyboard, start a rhythm section, and jam with congas, timbales, a horn section and a charanga flute.

It started after a trip to Little Havana in Miami, where the cafés on Calle Ocho have live Cuban music. This project is a way to play with those sounds.

Every sound is synthesized live with the Web Audio API. There are no audio samples, no build step and no dependencies. The whole app is a single `index.html`.

## Running it

Open `index.html` in a modern browser. That's it.

To serve it locally instead:

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000.

To publish it, turn on GitHub Pages for the repository (Settings → Pages → deploy from the `main` branch, root folder). The page is static, so nothing else is needed.

Browsers only allow sound after you interact with the page, so audio starts on your first click or key press.

## What's in the band

### Los cueros (drums)

| Instrument | Stroke | Key |
|---|---|---|
| Congas | Tumba (low, open) | `A` |
| | Conga (open tone) | `S` |
| | Conga (slap) | `D` |
| | Quinto (high) | `F` |
| Bongó | Macho (small drum) | `G` |
| | Hembra (large drum) | `H` |
| Timbales | Macho (high) | `J` |
| | Hembra (low) | `K` |
| | Cáscara (stick on the shell) | `L` |

### Pequeña percusión (small percussion)

| Instrument | Key |
|---|---|
| Claves | `Q` |
| Campana (bongo bell) | `W` |
| Mambo bell | `E` |
| Güiro, short scrape | `R` |
| Güiro, long scrape | `T` |
| Maracas | `;` |

### Metales y flauta (horns and flute)

| Section | Phrase | Key |
|---|---|---|
| Trompetas | Stab on the current chord | `,` |
| | Moña (two-trumpet riff) | `.` |
| | Caída (chord that falls away) | `-` |
| | Grito (high note with a lip shake) | `=` |
| Trombones | Moña de trombones (counter-riff to the trumpet moña) | `[` |
| | Tutti swell | `]` |
| Saxofones | Mambo saxes (tenor and baritone) | `\` |
| Flauta | Run | `/` |
| | Phrase | `'` |
| | Trino (trill) | `` ` `` |

While the band is playing, every horn and flute phrase waits for the next beat, so it always lands in time. Phrases also follow the tempo, the key and the current chord.

### Armonía (piano, tres, bass)

| Instrument | Keys |
|---|---|
| Piano | `1` to `0` |
| Tres cubano | `Z` to `M` |
| Baby bass | `Y` to `P` |

Notes are named the way Cuban musicians name them: Do, Re, Mi, Fa, Sol, La, Si. They follow the key you choose, so anything you play fits the band.

### Flute mode

Press `↑` to switch the keyboard to flute mode and `↓` to switch back. In flute mode:

| Keys | What they play |
|---|---|
| `1` to `0` | Flute notes. Hold a key to sustain the note. |
| `Z` | Guajeo, the repeating charanga figure |
| `X` | Llamada, two flutes calling the band in |
| `C` | Cascada, a two-octave run down |
| `V` | Floreo, a run up that ends in a trill |
| `B` | Adorno, grace notes and a turn |
| `N` | Pregón, a high syncopated answer |
| `M` | Danzón, a slow singing melody |

### Other controls

| Input | Effect |
|---|---|
| `Space` | Start or stop the band |
| `Shift` + any key or click | Ghost note (soft) |
| Click near a drum's rim | Louder, brighter stroke |
| Click near a drum's center | Softer stroke |

## The rhythm section

Press **Start the band** (or `Space`) and choose a style:

| Style | Tempo (BPM) | Notes |
|---|---|---|
| Son montuno | 80–120 | Anticipated bass tumbao, piano montuno, son clave |
| Cha-cha-chá | 100–132 | Steady cowbell and güiro, charanga flute |
| Bolero | 60–90 | Bongó martillo, maracas, arpeggiated piano |
| Guaguancó | 90–125 | Three congas, palitos, rumba clave |
| Mambo | 115–145 | Mambo bell, timbale fills, hard tumbao |
| Danzón | 80–110 | Cinquillo on the timbales, flute melody |

You can also:

- Switch the clave between **3‑2** and **2‑3**.
- Pick a **key** (Do, Re, Mi♭, Fa, Sol, La, Si♭) and one of five **chord progressions**, including a minor montuno.
- Turn individual parts on and off: claves, congas, bongó, timbales, bells, güiro, maracas, baby bass, piano montuno, flute guajeo and an improvising **flute soloist**.
- Watch the **clave check**. Hits that land on a clave stroke glow green on the step strip and are counted.

The room responds as well: the string lights come on as more parts join, the neon sign pulses on the beat, and each section of the band glows while it's playing.

## How the sounds are made

Everything is built from oscillators, noise and filters at play time:

- **Drums** are a pitched sine body with a falling pitch envelope, an overtone, and a burst of filtered noise for the skin. Harder hits get more noise, which makes them brighter.
- **Timbales and bells** stack inharmonic partials or detuned square waves through a band-pass filter.
- **Güiro** is a train of short noise ticks, and **maracas** are high-passed noise.
- **Tres** uses Karplus–Strong string synthesis, with a second slightly delayed string for each doubled course.
- **Piano** is additive synthesis with slightly stretched partials.
- **Brass** is detuned sawtooth waves with a filter that opens on the attack, plus a small pitch scoop. Falls, shakes and swells are pitch and envelope automation on the same voice.
- **Saxes** are sawtooth and square waves through a formant peak, with delayed vibrato.
- **Flute** is a sine with a little second harmonic, breath noise tuned to the note, a soft puff at the start, and vibrato that comes in as the note is held.

A small generated reverb gives everything a room sound, and a compressor on the output keeps it from clipping.

Timing uses a look-ahead scheduler that books notes on the audio clock a little ahead of time, so the groove stays steady even when the page is busy.

## Browser support

It's built for current versions of Chrome, Edge, Firefox and Safari, on desktop and mobile. Keyboard play needs a physical keyboard. On a phone or tablet, tap the instruments instead.

Key bindings use physical key positions, so they stay in the same place on non-US keyboard layouts.

## Project structure

```
index.html   the whole app: markup, styles and the audio engine
README.md
```
