# Sentinel Air Guitar

**Play air guitar for real.**

Sentinel Air Guitar puts a guitar in front of you through your webcam. Make chord shapes with the fingers of your fretting hand on the neck, and strum over the body with your other hand, just like the real thing. The camera reads both hands, and the guitar sounds like a guitar. It runs entirely in the browser: one HTML file, no install, no account.

### ▶ [Try the live demo](https://jameskeithharwood.com/sentinel-air-guitar/)

Works in a desktop or phone browser. Allow camera access, turn your sound up, and start strumming.

![Sentinel Air Guitar: an electric guitar on screen with a G chord shown on the fretboard and sparks flying off the strings](screenshot.png)

---

## What it is

A branch of [Sentinel Air Strings](https://github.com/jkh2/sentinel-air-strings). Instead of strings you place yourself, you get a complete six-string guitar:

- Real fret spacing, standard tuning (E A D G B E), and 12 frets.
- One rigid piece. You can move it and turn it to whatever angle is comfortable, and it never stretches, so the notes never change when you move it.
- Both hands play. Your fretting hand makes the chords, and your strumming hand strums.

## How to play

1. Open the page and tap **Start**. Allow camera access, and turn your sound up.
2. Hold your hands where they would be on a real guitar: fretting hand on the neck, strumming hand over the body. Your fretting hand shows in blue and your strumming hand in green.
3. **Make a chord.** Put your fingertips on the neck where the frets and strings are. The chord name appears above the neck, and green dots show where the chord's notes are.
4. **Strum.** Sweep your strumming hand across the strings over the body, down or up. The strings sound one after another in the order you cross them, like a real strum. Strum fast for loud, and slow for a gentle roll.
5. **Change chords** by changing the shape of your fretting hand. Strings that change note are damped as your fingers move, like lifting your fingers on a real guitar.

### Chord assist and real fretting

In the air, your fingers never land exactly on the strings. So by default, **Chord assist** looks at your finger shape and snaps it to the nearest real chord:

- Open chords: E, Em, E7, A, Am, A7, D, Dm, D7, C, C7, G, G7, B7
- Barre chords anywhere up the neck (E and A shapes, major and minor)
- Rock power chords on the three low strings

Turn Chord assist off in the **Guitar** menu for **Real fretting**. Then every fingertip plays exactly the string and fret it is on, and the highest fret on each string sounds. Moving a finger while a string is ringing gives hammer-ons, pull-offs, and slides.

The name above the neck is worked out from the notes that are actually sounding, so it stays correct with any tuning or capo.

### Moving the guitar

Tap **Move** (or press `G`). Then:

- Pinch, or drag with the mouse or a finger, anywhere on the body to move the guitar.
- Pinch or drag the headstock to turn it.

Tap **Done moving** to lock it in place. Moving is off while you play, because people often mime holding a pick, which looks like a pinch to the camera. Your position is remembered.

## Controls

| Control | What it does |
|---|---|
| **Move** (or `G`) | Unlocks the guitar so you can move and turn it. Tap again to lock it. |
| **Guitar** | Opens the guitar settings (see below). |
| **FX** (or `F`) | Opens the effects pedalboard. |
| **Music** (or `M`) | Opens the backing beat and looper. |
| **Camera** | Turns the camera image on or off. |
| **Skeleton** | Shows or hides the hand skeleton overlay. |
| **Camera picker** | Appears when you have more than one camera (webcam, DroidCam, GoPro, phone front and back). |
| **● Rec** (or `R`) | Records a clip of your playing with its sound. |
| **Hide menu** (or `H`) | Hides the buttons for a clean, full-screen view. Tap the small ☰ to bring them back. |
| **Haptics** | Phones only: a short buzz when you strum. |

### Guitar settings

| Setting | Options |
|---|---|
| **Tone** | **Rock** (overdriven amp, the default), **Crunch**, **Clean electric**, **Acoustic**. The tones are level-matched, so switching does not jump the volume. |
| **Tuning** | Standard, Half step down, Drop D, Open G |
| **Capo** | None, or frets 1 to 7 |
| **Chord assist** | On (snap to real chords) or off (real fretting) |
| **Left-handed** | Flips the guitar so the headstock points the other way |
| **Size** | Small, Medium, or Large |
| **Reset position** | Puts the guitar back in its starting place |

### Effects, beat, looper, and recording

Everything from Air Strings carries over:

- **Pedalboard:** Drive, Wah, Tremolo, Chorus, Flanger, Echo, Reverb, and Octave. The pedals sit in front of the guitar amp, like a real rig. On this guitar, the **Wah** follows how hard you play, opening up on loud strums like an envelope filter.
- **Backing beat:** Rock, Hip-hop, Dance, or Click, at 60 to 180 BPM.
- **Looper:** records what you play, synced to the beat, with up to six layers.
- **Clip recorder:** saves a video of you playing, with the sound.

See the [Air Strings README](https://github.com/jkh2/sentinel-air-strings#readme) for details on those.

### No camera? Use keys, a mouse, or touch

- Number keys pick chords: **1** G, **2** C, **3** D, **4** Em, **5** Am, **6** E, **7** A, **8** Dm, **9** F, and **0** for open strings.
- Move the mouse across the strings over the body to strum.
- On a touchscreen, press the neck with one finger to fret, and swipe across the strings with another to strum.

## How it works

| Piece | What it does |
|---|---|
| **Hand tracking** | [MediaPipe Hand Landmarker](https://ai.google.dev/edge/mediapipe/solutions/vision/hand_landmarker) finds both hands and 21 points per hand, in your browser. |
| **Which hand does what** | The hand nearer the headstock is the fretting hand, and the one over the body is the strumming hand. Left-handed mode flips the guitar. |
| **Reading frets** | Each fingertip of the fretting hand is mapped onto the guitar's own coordinates, then to the nearest string and the fret space it sits in, using real fret spacing. |
| **Chord assist** | Your fingertips are compared against every chord shape. The best fit wins, with a small preference for the chord you are already holding so it does not flicker. A new shape has to hold for a moment before it switches. |
| **Strumming** | Each frame, the app checks which strings your thumb, index, and middle fingertips crossed over the body, and in what order. Faster strums are louder and rake the strings faster. |
| **Sound** | Each string is synthesized with an extended Karplus-Strong model, with a pick-position notch and a sustain that depends on pitch and tone. It then goes through a guitar amp model with tone shaping and distortion. No audio files are used, and the tuning tests exact to the cent. |
| **One voice per string** | Strumming a string again replaces the note that was ringing on it, like a real guitar. |

The camera image is processed on your device. Nothing from your video is uploaded anywhere. The hand-tracking library and model are downloaded from public CDNs when the app loads, so you need an internet connection.

## Tips

- Use good, even lighting, and keep both hands fully in the camera's view.
- Your fretting fingers need to be visible to the camera. Holding the guitar more upright often helps the camera see them.
- If chords flicker, use **Size: Large** or move closer to the camera so the frets are bigger on screen.
- A bigger screen helps a lot. A phone running as a webcam (for example with DroidCam) and a computer monitor works well.

## Limits to know about

- The camera cannot tell if a finger is pressing or hovering. Any fingertip over the neck counts as fretting.
- The camera cannot see a finger lying flat across the strings, so a minor barre shape on the low E string plays as a power chord.
- Some chords differ by one finger moving one fret (D and Dm, A and Am). If tracking is shaky, assist may switch between them.

## Running it yourself

It is a single file named `index.html`, with no build step.

- **GitHub Pages:** upload `index.html` to a repo and enable Pages. It works over https.
- **Locally:** serve the folder from localhost, for example with `python3 -m http.server`, and open `http://localhost:8000`.

Browsers only allow camera access on https pages or localhost, so opening the file directly from your disk will not work.

## Troubleshooting

- **Camera message at the top:** it says why the camera did not start (blocked, not found, in use, or not https) and what to do.
- **"Hand tracking failed to load":** the tracking library could not be downloaded. Check your connection and reload. Number keys and the mouse still work.
- **No sound:** start with the Start button (browsers require a tap before playing audio), and check your volume.
- **The wrong hand frets:** move the guitar with **Move** so the neck is under your fretting hand and the body is under your strumming hand, or switch **Left-handed** in the Guitar menu.

## Built with

- [MediaPipe Tasks Vision](https://www.npmjs.com/package/@mediapipe/tasks-vision) for hand tracking
- Web Audio API for sound
- Canvas 2D for visuals
- Plain HTML, CSS, and JavaScript

## About

Part of the Sentinel family of projects by James Keith Harwood II, [Sentinel AI Systems](https://www.jameskeithharwood.com). Branched from Sentinel Air Strings, which grew out of the camera and body-tracking ideas in Sentinel Spotter.
