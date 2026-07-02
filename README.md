# Ledger

A pocket sight-reading drill for piano. Read the note (or notes) on the staff, tap the matching key — no installs, no accounts, just one HTML file you can host yourself and pull up on your phone.

**[Live demo →](https://craigdamlo.github.io/Ledger/)** *(update this link once it's deployed)*

## What it does

Shows notes on a treble or bass staff and waits for you to tap the matching key (or keys, in order) on an on-screen piano. Tracks your accuracy and streak, gives instant feedback, and can play back pitches so you connect what you're reading to what it sounds like. Everything is saved locally in your browser between visits — no account, no server.

No frameworks, no build step, no backend. It's a single `index.html` file with inline CSS/JS, plus two Google Fonts loaded from a CDN.

## All the settings, explained

Tap the gear icon (top right) to open settings. Here's what each one does:

### Drill picker
Five fixed drills to choose from:

| Drill | Range |
|---|---|
| Treble · In the staff | Within the treble staff lines, no ledger lines |
| Treble · + Ledger lines | Out to 3 ledger lines above/below the treble staff |
| Bass · In the staff | Within the bass staff lines, no ledger lines |
| Bass · + Ledger lines | Out to 3 ledger lines above/below the bass staff |
| Both clefs · Full range | Randomly mixes treble and bass, full range |

Switching drills resets any phrase progression back to 1 note (see below), so you're not thrown into a multi-note phrase in a brand-new drill.

### Progressive phrases
The core "difficulty ramp" feature. When on, rounds can show more than one note at a time — a short left-to-right melody instead of a single note — and the number of notes changes based on how you're doing. Turn it off and every round is always a single note, permanently.

When it's on, you pick **how** the note count changes, via three modes:

- **Streak-based** — every *N* correct answers in a row (you set *N*, default 5) bumps the note count up by one. Get one wrong and it drops back down by one. Same *N* required at every level.
- **Fixed thresholds** — set your own list of numbers, comma-separated (e.g. `3, 5, 8, 10`). The first number is how many correct in a row it takes to go from 1→2 notes, the second is 2→3, and so on — so you can make early jumps easy and later ones harder.
- **Fixed count** — no ramping at all. Set a number (1–5) and every round shows exactly that many notes, forever, regardless of right or wrong answers. Use this if you just want consistent multi-note practice without any adaptive difficulty.

Phrases cap out at 5 notes. The "Notes" stat (in the stats row above the staff) shows your current count and, in streak/threshold modes, your progress toward the next bump (e.g. `2 (3/5)`).

### Sharps & flats
Mixes accidentals into about a third of notes when on. The black keys become real, tappable targets (labeled with both spellings, e.g. "C♯ / D♭") when this is active. Turn it off to drill naturals only.

### Sound
Plays the actual pitch of whatever key you tap, using the Web Audio API — no audio files, just synthesized tones. On by default; useful for connecting what you're reading to what it should sound like.

### Play note on appear
When on, automatically plays the pitch (or, for phrases, the whole short melody in sequence) as soon as a new note/phrase appears — before you've answered. **Off by default** on purpose: hearing the answer up front lets you match by ear instead of actually reading the staff, which works against the point of a sight-reading drill. Turn it on if you specifically want combined ear-training.

Independent of this, you can always tap the staff card itself to hear the current note/phrase played on demand, any number of times — that's not gated by this setting.

### Show key letters
Shows the letter name on every key (and both spellings on black keys). Middle C is always labeled regardless of this setting, marked with a small gold dot so you've always got an anchor point. Turn this off once you can find notes without the training wheels.

## Hosting it on GitHub Pages

1. Create a repo (public, e.g. `ledger-sight-reading`).
2. Upload `index.html` to the repo root (Add file → Upload files → commit).
3. Go to **Settings → Pages**. Under "Build and deployment," set Source to **Deploy from a branch**, branch **main**, folder **/ (root)**. Save.
4. Wait a minute or two — your site will be live at `https://yourusername.github.io/ledger-sight-reading/`.

Add it to your phone's home screen (Share → "Add to Home Screen" on iOS, browser menu on Android) and it opens full-screen like a regular app.

## Customizing

Everything lives in `index.html`. A few starting points if you want to tweak it:

- **Drill ranges** — the `LEVELS` array near the top of the `<script>` block. Each level has `diffMin`/`diffMax`, which control how far above/below the staff lines notes can land.
- **How often accidentals show up** — `ACCIDENTAL_PROB` (currently 0.35, i.e. ~35% of notes).
- **Max phrase length** — `MAX_PHRASE_NOTES` (currently 5).
- **Default ramp settings** — `DEFAULT_FIXED_THRESHOLDS` for the fixed-thresholds mode, or the initial values in the `state` object for streak-per-level and fixed note count.
- **Colors / fonts** — the CSS custom properties at the very top of `<style>` (`--bg`, `--brass`, `--correct`, `--wrong`, etc.).
- **Feedback timing** — in `handleAnswer()`, the `delay` calculation controls how long the correct/wrong message stays up before the next round starts.
- **Note spacing on the staff** — `PREF_NOTE_SPACING` and the `NOTE_AREA_LEFT`/`NOTE_AREA_RIGHT` constants control how tightly notes cluster in a phrase and where the group centers.

## License

Do whatever you want with it — it's yours.
