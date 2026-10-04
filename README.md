# Circle of Fifths – MIDI Visualizer

A simple, browser-based music tool that helps you **see and hear the relationship between notes, scales, and the circle of fifths**.

Play notes from a MIDI keyboard, your computer keyboard, the on-screen piano, or directly from the circle. The visualizer shows each note as a **scale degree relative to the tonic**, making it easier to understand intervals, scales, and chord shapes.

> **No installation or build step required.** The entire app runs from a single HTML file.

---

## 🎵 What can you do with it?

### Choose a major or minor scale

Select either **Major** or **Minor**, then choose any of the 12 tonic notes.

The circle updates its scale-degree and note-name labels according to the selected key and mode.

### 🎹 Play notes in real time

You can play using:

- A USB MIDI keyboard
- Your computer keyboard
- The built-in two-octave piano
- The note circles themselves

Every note you play is immediately reflected on the circle.

### 🌀 Explore the Circle of Fifths

The notes are arranged according to the circle-of-fifths relationship.

Instead of simply showing note names, the visualizer shows the notes as **scale degrees relative to the selected tonic**. This means the same interval relationships can be recognised even when you change keys.

For example, once a tonic is selected, the circle can show degrees such as:

`I · ♭II · II · ♭III · III · IV · ♭V · V · ♭VI · VI · ♭VII · VII`

In minor mode the labels follow the minor scale, so you see `III`, `VI` and `VII` instead of `♭III`, `♭VI` and `♭VII`.

The scale tones are visually distinguished from the non-scale tones.

### 🔊 Built-in sound

You don't need a MIDI keyboard just to hear the notes.

The app includes a Web Audio synthesizer with four instrument sounds:

- Piano-like
- Soft pad
- Organ
- Synth

Choose **None** to mute the keys. The **Master volume** slider controls the keys and the tanpura together.

### 🪕 Tanpura drone

The **Tanpura** button plays a looping, plucked-string drone tuned to the current tonic while you practice.

This is useful for ear training because you hear every note you play against a constant tonal centre.

How it sounds:

- Four strings are plucked in a repeating cycle: **Pa**, **Sa**, **Sa**, then the **low Sa**.
- Pa is a perfect fifth above the low Sa; the two Sa strings sit an octave above it.
- Each pluck starts soft and gradually brightens, with a shimmering buzz similar to the *jivari* bridge of a real tanpura.
- All strings share one tone colour and a short room echo, so they blend into a single instrument.

You can:

- Turn the tanpura on or off
- Change how fast the strings are plucked with the **Speed** slider (0.5× to 2×, default 1×, about 4 seconds per full cycle)
- Change the tonic and have the tanpura follow it (the old key fades out as the new one starts)
- Use it while playing from MIDI, the computer keyboard, the piano, or the circle
- Set its loudness with the **Master volume** slider (shared with the keys)

The tanpura is **off by default**.

### 🎯 Set the key by ear

Don't want to manually select the tonic?

Click:

**Set key by ear**

Then play a note. That note becomes the tonic automatically.

### 💡 Visual feedback

When a note is played:

- Its circle lights up
- A coloured glow appears around it
- Its scale-degree label becomes highlighted
- The corresponding note on the on-screen piano lights up
- Multiple held notes are connected to form a shape
- The centre of the circle shows the Roman numeral of the chord you hold

This makes intervals and chord shapes easier to see.

### 🎼 Chord detection and history

When you hold three or more notes that form a triad, the centre of the circle shows its Roman numeral relative to the tonic:

- Uppercase for major (`I`, `V`), lowercase for minor (`vi`, `ii`)
- `°` for diminished and `+` for augmented
- `sus2` and `sus4` for suspended chords

Each chord is also added to a scrolling **chord history**, grouped into sections by key and mode (for example "C Major"). Changing the key or mode starts a new section.

Turn on the **Note names** button to see the note names on the circle and under the chord numeral.

---

## ✨ Features

- **Major / Minor selection** – switch between major and minor scales.
- **12 tonic choices** – select any root note.
- **Scale-degree visualization** – view notes relative to the selected tonic.
- **Circle-of-fifths layout** – notes are arranged by fifths rather than chromatic order.
- **Automatic note spelling** – note names adapt to the selected key and mode.
- **Set key by ear** – use the next played note as the tonic.
- **Tanpura drone** – a looping Pa–Sa–Sa–Sa tanpura on the tonic, with a speed control, for ear training.
- **Web MIDI support** – connect compatible MIDI keyboards directly in the browser.
- **Built-in synthesizer** – Piano-like, Soft pad, Organ, and Synth sounds.
- **Two-octave on-screen piano** – play without external hardware.
- **Computer keyboard input** – use your keyboard as a simple piano.
- **Octave shifting** – use `Z` and `X` (or the on-screen arrows) to move the playable range.
- **Note-name display** – show note names on the circle with the **Note names** button.
- **Chord/interval visualization** – held notes form a shape on the circle.
- **Chord detection** – held triads (major, minor, diminished, augmented, sus2, sus4) appear as Roman numerals in the centre.
- **Chord history** – played chords are listed in order, grouped by key and mode.
- **Responsive interface** – works across desktop and mobile-sized screens.
- **No build system** – one HTML file contains the application.
- **No backend** – everything runs locally in the browser.

---

## 🚀 Quick start

### Use the online version

Open the deployed website in a modern browser and start playing.

### Run locally

Clone the repository:

```bash
git clone https://github.com/MstYuta/circle-of-fifths-midi.git
cd circle-of-fifths-midi
```

Start a local web server:

```bash
python3 -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

For MIDI access, use a browser that supports Web MIDI and allow MIDI access when prompted.

---

## 🎹 Computer keyboard

The computer keyboard provides a convenient way to play without a MIDI controller.

```text
       W E     T Y U     O P
      ───────────────────────
       A S D F G H J K L ; '

       C D E F G A B C D E F
```

| Key | Action |
| --- | --- |
| `A W S E D F T G Y H U J K O L P ; '` | Play notes |
| `Z` | Move down one octave |
| `X` | Move up one octave |

The exact playable range follows the currently selected octave.

---

## 🌀 Understanding the visualizer

The visualizer separates two ideas:

### 1. Pitch relationship

Each incoming note is compared with the selected tonic.

```text
degree = (pitchClass - tonic + 12) % 12
```

This determines the note's chromatic distance from the tonic.

### 2. Circle-of-fifths position

The resulting degree is positioned around the circle using:

```text
position = (degree × 7) % 12
```

Because 7 semitones is a perfect fifth, this places the notes in circle-of-fifths order.

The angular position is then:

```text
angle = position × 30°
```

So the application combines **interval/scale-degree information** with the familiar **circle-of-fifths arrangement**.

---

## 🎼 Major and minor modes

The app currently supports:

### Major

```text
1  2  3  4  5  6  7
```

### Minor

```text
1  2  ♭3  4  5  ♭6  ♭7
```

The selected mode affects:

- The available tonic names
- Note spelling
- Which degrees are treated as scale tones
- Roman-numeral labels (`III`, `VI`, `VII` in minor)
- The visual emphasis and background colours of the circle

---

## 🪕 Tanpura

The tanpura is designed primarily as an **ear-training aid**.

For example, if the tonic is `C`, the tanpura plucks `G`, `C`, `C` and a low `C` in a loop. This gives you a steady tonal centre while you play other notes.

This allows you to hear relationships such as:

```text
C → E     major 3rd
C → G     perfect 5th
C → B     major 7th
C → F     perfect 4th
```

The tanpura automatically follows the selected tonic. Use the **Speed** slider to make the plucking slower or faster.

---

## 🎹 MIDI keyboard support

The application uses the browser's **Web MIDI API**.

To connect a MIDI keyboard:

1. Connect your MIDI keyboard to the computer.
2. Open the application in a supported browser.
3. Click **Connect MIDI keyboard**.
4. Allow MIDI access when the browser asks.
5. Play your keyboard.

The visualizer supports:

- Multiple MIDI channels
- Note velocity
- Multiple simultaneous notes
- Repeated pitches in different octaves
- MIDI note-off messages
- Multiple MIDI sources

---

## 🌐 Browser support

| Browser | Visualizer & Sound | MIDI |
| --- | --- | --- |
| Chrome – desktop | ✅ | ✅ |
| Edge – desktop | ✅ | ✅ |
| Opera – desktop | ✅ | ✅ |
| Chrome – Android | ✅ | ✅ USB |
| Firefox 108+ | ✅ | ✅ |
| Safari | ✅ | ❌ Web MIDI unavailable |
| iOS / iPadOS browsers | ✅ | ❌ Web MIDI unavailable |

Even when MIDI is unavailable, you can still use:

- The on-screen piano
- Computer keyboard controls
- Clickable notes on the circle
- Built-in sound

### 🍎 Using a MIDI keyboard with Safari on macOS

Safari currently does not provide native Web MIDI support. If you are using **Safari on a Mac** and want to connect a physical MIDI keyboard, there is a workaround using the **Web MIDI API extension from Jazz-Soft**.

The extension provides Web MIDI API support to browsers that do not implement it natively. According to Jazz-Soft, the Safari version requires **Jazz-MIDI** as a companion component.

#### Setup

1. Open the [Jazz-Soft Web MIDI API extension page](https://jazz-soft.net/download/web-midi/).
2. Follow the **Safari** installation instructions for the **Web MIDI API extension**.
3. Install or enable the required **Jazz-MIDI** component when prompted.
4. Restart Safari if required.
5. Connect your MIDI keyboard to your Mac.
6. Open the Circle of Fifths MIDI Visualizer.
7. Click **Connect MIDI keyboard** and allow MIDI access if Safari asks.
8. Start playing.

This workaround is provided by a third party and is **not part of this project**. Availability and compatibility may change as Safari and macOS are updated.

> **Recommended alternative:** If you don't want to install the Safari workaround, use the latest **Chrome, Edge, Opera, or Firefox** on macOS. These browsers provide native Web MIDI support.

For the latest Safari workaround and compatibility information, see the [Jazz-Soft Web MIDI API extension documentation](https://jazz-soft.net/download/web-midi/).

---

## 📁 Project structure

The project intentionally stays lightweight:

```text
circle-of-fifths-midi/
│
├── index.html      # Complete application
├── README.md       # Project documentation
└── LICENSE         # MIT License
```

The HTML file contains the application's:

- HTML structure
- CSS styling
- Circle-of-fifths visualization
- MIDI handling
- Web Audio synthesizer
- Tonic and mode selection
- Tanpura drone (with speed control)
- On-screen piano
- Computer keyboard controls

The only external resource requested by the page is the **Inter font from Google Fonts**. A system-font fallback is provided if it cannot be loaded.

---

## 🌐 Deployment

### GitHub Pages

The project can be deployed directly using GitHub Pages:

1. Push the repository to GitHub.
2. Open **Settings → Pages**.
3. Select the `main` branch.
4. Select the repository root as the folder.
5. Save the settings.

GitHub Pages serves the site over HTTPS, which is important for browser MIDI access.

The project can also be deployed using services such as Netlify, Vercel, or Cloudflare Pages.

---

## 🛠️ Current limitations

- The built-in sounds, including the tanpura, are synthesised rather than sampled instruments.
- The tanpura uses a fixed Pa–Sa–Sa–Sa tuning and has no volume control of its own; a speed change takes effect from the next pluck.
- Sustain pedal input is not currently handled.
- Web MIDI is unavailable in Safari and iOS/iPadOS browsers.
- Some browsers keep audio muted until the user interacts with the page.
- The visualizer is primarily designed around pitch classes and scale degrees rather than full music notation.

---

## 💭 Possible future improvements

Some ideas for future development:

- Richer chord detection (seventh chords, extensions, chord names)
- Automatic key/mode detection
- Sustain-pedal support
- Alternative tanpura tunings (such as Ma) and an independent tanpura volume
- Sampled piano and instrument sounds
- Light/dark visual themes
- More advanced ear-training exercises
- Additional scale types
- Improved chord and interval analysis

---

## 🤝 Contributing

Contributions and ideas are welcome.

A simple workflow for contributing:

```bash
git clone https://github.com/MstYuta/circle-of-fifths-midi.git
cd circle-of-fifths-midi

git switch -c feature/your-feature

# Make your changes

git add .
git commit -m "Add your feature"
git push -u origin feature/your-feature
```

Then open a **Pull Request** on GitHub.

---

## 📄 License

This project is licensed under the **MIT License**.

See [`LICENSE`](LICENSE) for the full license text.
