# Ledger

A pocket sight-reading drill for piano. Read the note on the staff, tap the matching key — no installs, no accounts, just one HTML file you can host yourself and pull up on your phone.

**[Live demo →](https://craigdamlo.github.io/Ledger/)** *(update this link once it's deployed)*

## What it does

- Shows a single note on a treble or bass staff and waits for you to tap the matching key on an on-screen piano
- Five drills: Treble in-staff, Treble + ledger lines, Bass in-staff, Bass + ledger lines, and Both clefs / full range
- Optional sharps & flats — mixed in at random, with the matching black key as the target
- Immediate feedback: the key you tap flashes green (correct) or red (wrong), and the correct key always lights up green so you can see what you missed
- Middle C is permanently marked on the keyboard (gold dot + label) and the keyboard auto-centers on it for every drill
- Tracks streak, best streak, and accuracy, saved locally in your browser between visits
- "Show key letters" toggle for training wheels — turn it off once you're finding notes by feel

No frameworks, no build step, no backend. It's a single `index.html` file with inline CSS/JS, plus two Google Fonts loaded from a CDN.

## Hosting it on GitHub Pages

1. Create a repo (public, e.g. `ledger-sight-reading`).
2. Upload `index.html` to the repo root (Add file → Upload files → commit).
3. Go to **Settings → Pages**. Under "Build and deployment," set Source to **Deploy from a branch**, branch **main**, folder **/ (root)**. Save.
4. Wait a minute or two — your site will be live at `https://yourusername.github.io/ledger-sight-reading/`.

Add it to your phone's home screen (Share → "Add to Home Screen" on iOS, browser menu on Android) and it opens full-screen like a regular app.

## Customizing

Everything lives in `index.html`. A few starting points if you want to tweak it:

- **Drill ranges** — the `LEVELS` array near the top of the `<script>` block. Each level has `diffMin`/`diffMax`, which control how far above/below the staff lines notes can land (0–8 = within the staff, negative/beyond-12 = ledger lines).
- **How often accidentals show up** — `ACCIDENTAL_PROB` (currently 0.35, i.e. ~35% of notes).
- **Colors / fonts** — the CSS custom properties at the very top of `<style>` (`--bg`, `--brass`, `--correct`, `--wrong`, etc.).
- **Feedback timing** — in `handleAnswer()`, the `delay` value controls how long the correct/wrong message stays up before the next note appears.

## License

Do whatever you want with it — it's yours.
