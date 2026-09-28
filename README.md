# Circle of Fifths – MIDI Visualizer

Play a MIDI keyboard and watch every note light up on the **circle of fifths**, shown as **scale degrees** relative to a tonic you choose. Runs entirely in the browser: one HTML file, no build step, no dependencies.

<!-- Add a screenshot or GIF here: docs/demo.gif -->

## Features

- **Tonic selection** – pick any of the 12 root notes, or press *Set tonic from next note* and play it.
- **Scale-degree view** – the circle is laid out in fifths (1, 5, 2, 6, 3, 7, ♯4, ♭2, ♭6, ♭3, ♭7, 4). Each note you play is shown relative to the tonic, so the same shape means the same thing in every key.
- **Glow feedback** – a played note glows in its own colour, its label turns white, and a shape joins all held notes so chords are easy to recognise. The centre shows the held degrees and note names.
- **Web MIDI input** – plug-and-play with class-compliant USB MIDI keyboards, including velocity and multi-channel devices.
- **Built-in sound** – a Web Audio synth with four instruments (Piano-like, Soft pad, Organ, Synth) and a volume control.
- **Two-octave on-screen piano** – it lights up for every note from any source (MIDI, computer keys, mouse, or the dots) in the colour of that note's scale degree.
- **Octave shifting** – `Z` goes down an octave, `X` goes up. The default range is C3–C5.
- **No MIDI keyboard needed** – play with the computer keyboard, the on-screen piano, or by clicking the dots.
- **Clear MIDI messages** – status light and guidance for blocked permission, no device found, unsupported browser, and non-HTTPS pages. MIDI permission is only requested when you click **Connect MIDI keyboard**.

## Quick start

1. Open `index.html` in Chrome, Edge or Opera. (Serve it over `https://` or `http://localhost`; browsers block MIDI on other pages.)
2. Click **Connect MIDI keyboard** and choose **Allow**.
3. Pick a tonic and play.

To run locally:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Computer keyboard layout

```
 W E   T Y U   O P
A S D F G H J K L ; '
C D E F G A B C D E F      (semitones from C of the current octave)
```

| Key | Action |
| --- | --- |
| `A W S E D F T G Y H U J K O L P ; '` | Play notes (C to F, about 1.5 octaves) |
| `Z` / `X` | Octave down / up |

## Browser support

| Browser | Visualizer and sound | MIDI keyboard |
| --- | --- | --- |
| Chrome, Edge, Opera (desktop) | Yes | Yes |
| Chrome (Android) | Yes | Yes (USB) |
| Firefox 108+ | Yes | Yes (may ask to install a site-permission add-on) |
| Safari, iOS/iPadOS browsers | Yes | No (Web MIDI is not supported) |

Where MIDI is unavailable, the on-screen piano, computer keys and clickable dots still work.

## How it works

Each incoming MIDI note is reduced to a pitch class and converted to a scale degree:

```
degree   = (pitchClass - tonic + 12) % 12
position = (degree * 7) % 12        // steps around the circle of fifths, clockwise from the top
angle    = position * 30°
```

Multiplying by 7 semitones (a perfect fifth) modulo 12 puts the degrees in circle-of-fifths order. Held notes are tracked per source (device, MIDI channel and note number), so chords, repeated pitches in different octaves and multi-channel devices work correctly.

## Project structure

```
index.html   # the whole app: HTML, CSS and JavaScript
README.md
```

The only external request is the Jost font from Google Fonts, which falls back to system fonts if it can't load.

## Deploy

**GitHub Pages:** push `index.html` to a repository, then go to *Settings → Pages*, choose the `main` branch and root folder. The site is served over HTTPS automatically.

Netlify, Vercel and Cloudflare Pages also work by dropping in the folder.

## Known limitations

- The sound is a simple synthesizer, not sampled instruments.
- The sustain pedal is not handled yet.
- Web MIDI is not available in Safari or on iOS.
- If you play your MIDI keyboard before touching the page, browsers keep audio muted until the first click or key press.

## Ideas for later

- Chord-name and key/mode detection
- Sustain pedal support
- Sampled piano sounds
- Light theme

## License

MIT – see `LICENSE`. (Add a `LICENSE` file, or change this line to the licence you prefer.)
