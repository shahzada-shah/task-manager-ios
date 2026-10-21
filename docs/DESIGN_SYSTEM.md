# Design system · Volt on ink

## Colour

| Token | Hex | Use |
|---|---|---|
| `volt` | `#D8F558` | The one accent on dark and ink surfaces |
| `voltOnLight` | `#B7D62C` | The accent on light surfaces |
| `ink` | `#15170C` | Dark surfaces, text on volt |
| `paper` | `#F1F0E5` | Light background, deeper than white so cards pop |
| `tide` | `#4E8D8C` | In progress, running timer |
| `ember` | `#E85C24` | Late, destructive |
| `olive` | `#5A6F4A` | Quiet accents |
| `amber` | `#D99A2B` | Secondary highlight |

Light mode is its own palette, not an inverted dark mode: white cards on paper, three text stops (`#16160F`, `#3A3A30`, `#6E6E5D`).

## Type

- **Besley** for dates and milestone numbers only.
- **Schibsted Grotesk** for everything else.

## Rules

- Light mode: volt appears on the add button and the bars only. Active tabs use a tint chip, never a dot.
- Light cards are borderless with a soft shadow; hairlines return in dark mode.
- Checkboxes are squircles, echoing Tick's body.
- Press feedback (a short squash), never hover.
- Undo lives in the toast, never inside rows. Swipe backdrops appear only mid-drag.
- Drawn icons only. No emoji.

## Tick

One closed path: three soft tufts on a mound base, ink features on volt. Six moods (happy, proud, focused, sleepy, cheer, grumpy), each tied to one app state with one idle animation. The tiled crop, with the base bleeding off a squircle, is the app icon.
