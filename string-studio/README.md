# String Studio

A browser-based virtual guitar you play with your laptop touchpad (or mouse, or keyboard, or touchscreen). No audio samples — every note is synthesized live in the browser using the Karplus-Strong algorithm.

**[Live demo](#)** — replace this with your GitHub Pages link once enabled (see repo root README for setup).

## How to play

- **Slide** a finger/cursor across the strings to strum
- **Tap** a single string to pluck it
- **Hold still** near a ringing string to mute it (palm mute)
- **Keyboard fallback:** number keys `1`–`6` pluck each string (high E to low E), `spacebar` mutes everything
- Downstrokes sound brighter, upstrokes sound warmer — try both directions
- Hit **Record**, play something, hit **Stop** to get a downloadable `.wav`

## How it works

- **Sound:** Web Audio API, Karplus-Strong synthesis (feed noise through an averaging feedback loop → it settles into a plucked-string tone). No `.mp3`/`.wav` sample files anywhere. Buffers are pre-generated once at startup so nothing synthesizes mid-play.
- **Gestures:** Pointer Events with `getCoalescedEvents()` for segment-crossing detection, so fast swipes don't skip strings. True multi-touch isn't possible on trackpads via web APIs (the OS collapses gestures to a single cursor), so multi-finger picking is out of scope here by design, not oversight.
- **Visuals:** Canvas, damped standing-wave animation per string, respects `prefers-reduced-motion`.
- **Recording:** Raw PCM captured via `ScriptProcessorNode`, hand-encoded into a real WAV file on stop.

## Stack

Plain HTML/CSS/JS, single file, zero build step, zero dependencies. Fonts loaded from Google Fonts CDN.

## Known limitations

- No true multi-touch (trackpad hardware/API limitation, not fixable from the browser)
- One instrument (guitar) — this was scoped as the MVP; violin, ukulele, harp etc. were cut for a later pass
- `ScriptProcessorNode` is deprecated in favor of `AudioWorklet` — kept for simplicity, worth migrating for a longer-lived version

## Run it locally

Just open `index.html` in a browser. No server needed.
