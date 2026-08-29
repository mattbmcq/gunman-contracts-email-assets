# gunman-contracts-email-assets

Image host for the *Gunman Contracts – Stand Alone* launch email.

Same pattern as `downshot-email-assets` and `hidepaint-email-assets`: a public
GitHub repo served through GitHub Pages, so every `src` in the email resolves
without a login. **Do not host these on Google Drive.** `lh3.googleusercontent.com`
links fail in Gmail and Outlook often enough to sink a send, which is why both
prior campaigns moved off Drive.

**Published 29 Aug 2026.** Live at:

```
https://mattbmcq.github.io/gunman-contracts-email-assets/<file>
```

Pages serves from `main` at the repo root, the same arrangement as the two prior
campaigns. The email already points at these URLs and all eleven files were
verified returning 200 with the right content type.

Anything committed here is **public and reachable by anyone who has the URL**.
That is the trade every one of these campaigns makes, because an email client
will not authenticate to fetch an image. Nothing is linked or indexed, but do
not treat it as private.

## Where these came from

Everything here is now **official art supplied by the owner on 29 Aug 2026**.
Nothing is recovered out of a PDF any more.

- **Brand pack** — Dropbox folder "Gunman Contracts Assets For Email", shared by
  Michael Cussell, three subfolders (`Artwork`, `GIFS`, `Screenshots`).
- **GIFs** — also delivered directly at `F:\More 2080 Storage\Gunman`. Byte-for-byte
  identical to the ones in the Dropbox `GIFS` folder, so either source is fine.
- **Social glyphs** — copied from `downshot-email-assets`.

## Manifest

Filenames are what `docs/gunman-launch-email.html` asks for. Do not rename them
without changing the template.

| File | What it is | Status |
|---|---|---|
| `hero.jpg` | Header cover art, 1320x562, 113 KB | **Done** |
| `gmc-main.gif` | Body GIF 1, 400x95 | **Done.** Fade trimmed, see below |
| `gmc-story.gif` | Body GIF 2, 400x95 | **Done.** Fade trimmed, see below |
| `gmc-hive.gif` | Body GIF 3, 400x95 | **Done.** Opens on the Hive interior |
| `logo-2080.png` | 2080 mark above the footer copyright, 180x212 | **Done** |
| `logo.png` | Title lockup, 1200x961, real alpha | **Done, held in reserve** |
| `discord.png` | Footer icon, 80x80 white on transparent | **Done** |
| `youtube.png` | Footer icon | **Done** |
| `tiktok.png` | Footer icon | **Done** |
| `instagram.png` | Footer icon | **Done** |
| `x.png` | Footer icon | **Done** |
| ~~`steam.png`~~ | Footer icon | **No longer used.** The icon was removed from the email |

`logo.png` is not referenced by the email, because `hero.jpg` already carries the
lockup. It is kept because it is the transparent version that was missing for a
week, and because any future layout that needs the mark on its own now has it.

## The black first frames were fixed here

`gmc-main.gif` and `gmc-story.gif` both opened on a fade from black. Outlook
2007 through 2019 on Windows renders only the **first** frame of an animated
GIF, so on those clients a recipient saw a black rectangle with a caption under
it and nothing else.

Rather than wait on a re-export, `docs/gif-trim-lead.js` in the main repo
removes the fade. It cannot simply delete frames, because GIF frames are deltas
and every frame in these files carries a transparent index, so cutting the front
off leaves holes. Instead it decodes the frames, composites them, finds where
the fade stops climbing, re-encodes **that composited state** as one opaque
frame, and keeps every later frame byte for byte.

Five lead frames came off each file and **both files got smaller**.
`gmc-hive.gif` needed nothing, it already opened on the Hive interior.

| File | Now opens on | Bytes |
|---|---|---|
| `gmc-main.gif` | A pistol and laser sight | 2588878 → 2579751 |
| `gmc-story.gif` | The warehouse district in the rain | 2387961 → 2358725 |

The untouched originals are kept beside them as `gmc-main.orig.gif` and
`gmc-story.orig.gif`. **Do not wire those into the email**, and do not publish
them, they are only there so the change is reversible.

Re-run it if new GIFs arrive, before publishing them:

```
node docs/gif-trim-lead.js gmc-main.gif          # in place, keeps a .orig.gif
node docs/gif-trim-lead.js gmc-main.gif --check  # report only
```

Two improvements are still worth having and neither blocks the send:

- **Size.** Roughly 7.3 MB across the three. That does not touch the Gmail
  clipping limit, which counts HTML and not images, but it is a slow load on
  mobile data. A smaller palette or a lower frame rate would help.
- **Resolution.** 400px wide displayed at 612px is a 1.53x upscale and reads
  soft. Exports at 800x190 would drop straight in.

## What was removed on 29 Aug

Deleted, because the official art supersedes them and leaving broken files in a
repo that is about to be public is asking for one to get used by accident:

- `contract-01-outpost.jpg`, `contract-02-warehouse.jpg`, `contract-03-dinner-out.jpg`
  — extracted from the 21 Aug PDF, carried white and black artifacts where the
  soft mask was dropped. The GIFs replace them.
- `logo-lockup-DO-NOT-USE-white-corners.jpg` — the flattened lockup. `logo.png`
  replaces it with real alpha.
- `bg-texture.jpg` — the improvised header ground. `hero.jpg` replaces it.

`trailer-thumb.jpg` was never made and is no longer needed. The trailer is a
button now. `steam.png` was never made either, and the Steam social icon was
removed from the email rather than held for it, because the store link directly
below the icon row already carries that destination.

Also in the Dropbox pack and deliberately **not** copied here: ten 4K
screenshots and `GMC - Logo - withShadow.png`. The three GIFs carry the footage
load in the email and the brief was to keep it compact, so the screenshots stay
in the press pack where a recipient can take the ones they want.

## Design tokens

Sampled from the rendered press kit pages, not eyeballed. The email uses these
exact values.

| Token | Use |
|---|---|
| `#e89830` | Accent. Every heading, every label, both buttons |
| `#172226` | Card ground, the dominant pixel in the source |
| `#101a1d` | Outer ground |
| `#1d2a2f` | Inset panels |
| `#2b393e` | Rules |
| `#d0d2d3` | Body text. Cool grey, not warm |
| `#ffffff` | Bold emphasis inside body copy |
| `#8e999c` | Captions and muted labels |

Typeface is **Rajdhani** (Medium 500, Semibold 600, Bold 700), read from the
press kit font table. It is a Google font, linked in the email for clients that
honour webfonts, falling back to Trebuchet MS. Never let layout depend on it.

## One email, both audiences

Press, influencers, PC and VR all receive the same email, so there is **one**
set of images and each has to work for a reader in either mode. Favour footage
where the input method is not the subject. Keep headsets and motion controllers
out of the header.

## Before committing anything else

Pages is already enabled, so **a new file is public the moment it is pushed.**
There is no staging step. Nothing pre-embargo goes in until it is cleared to be
seen, and filenames are public too, so do not name a file after an unannounced
date, platform or partner.

The three GIFs are gameplay, and the gameplay embargo does not lift until
launch. They are here because an email client will not authenticate to fetch an
image, which is the same trade the Downshot and Hide and Paint campaigns made.
Nothing links to them and nothing indexes them, but they are reachable. If that
is not acceptable to Arne, the alternative is an email with no footage in it.
