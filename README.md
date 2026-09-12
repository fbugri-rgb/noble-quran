# The Noble Quran — site

The marketing site for **The Noble Quran**, a Quran reader for iPhone.

Live at **https://fbugri-rgb.github.io/noble-quran/**

This repository holds the site only. The app's own source is not public.

```
index.html     the landing page
privacy.html   what the app records, and why
support.html   common questions and where to report a problem
style.css      tokens, typography, masthead, buttons, footer
img/           the icon, and screenshots of the app
```

Static HTML and CSS. No build step, no dependencies, nothing to install.

```sh
python3 -m http.server 8000     # then open http://localhost:8000
```

## Two things on the page are the app, not pictures of it

**The cover** in the hero is a `<canvas>`. It draws the app's own cover artwork
and tints it per metal, so dragging the scrubber genuinely walks it through iron
→ bronze → silver → gold → platinum and the seven worked steps inside each. The
breath, the crossing gleam and the glints are the treatment the app uses, and the
glints are sampled from bright pixels in the artwork rather than scattered, so
one never lands on flat ground. It animates only while on screen, and not at all
under `prefers-reduced-motion`.

**The pinned reader** is a real page, not a screenshot: the Uthmani text of
Al-ʿAsr, the real tajweed markup from AlQuran Cloud's `quran-tajweed` edition,
and the app's own seventeen rule colours. That is why it can add a layer as you
scroll — translation, then colour in the letters, then the juz band, then the
recitation walking a word along the last verse — instead of swapping an image.

Do not hand-write the tajweed colouring. Take it from the edition, in the
`[code[letters]` form the app itself parses, or it will be wrong.

## Previewing one scroll step

The feature section is pinned, so its later states are only reachable by
scrolling to exactly the right place. `?step=N` pins one and leaves the scroll
observer off:

```
?step=0   Arabic alone
?step=1   + translation
?step=2   + tajweed
?step=3   + juz and quarter band
?step=4   + following the recitation
```

## The link preview

`img/og.jpg` is what appears when the site is shared. It is rendered from
`og.html` rather than drawn in a script, so it uses the site's own typefaces and
palette instead of an approximation:

```sh
python3 -m http.server 8000
chrome --headless --window-size=1200,630 --force-device-scale-factor=2 \
       --screenshot=og_raw.png http://localhost:8000/og.html
# then downscale og_raw.png to 1200×630 and save as img/og.jpg
```

Edit the copy in `og.html` and re-render; do not retouch the JPEG.

## The Arabic in the Makharij section

Each Arabic letter set inline with English is wrapped in `<bdi>`. Without it
the bidirectional algorithm reorders them across the Latin words and the
sentence comes out saying the wrong thing — "ص is not س, ح is not ه" rendered
as "ص is not ح, س is not ق". It looks like a typo and is not one. Any new
sentence mixing single Arabic letters into English needs the same treatment.

## Images

`img/cover_*.webp` are **real captures of the app**, one per metal, taken by
the screenshot driver in the app repo with the reading days seeded to the last
step of each metal. They were previously Python tints of a single screenshot;
they are not any more, so they show the backlight behind the medallion and the
Name lighting at platinum exactly as the app draws them.

Regenerate all five together, never one at a time — the fan shows them side by
side and a mismatched one would stand out.

`img/shot_reader.webp` is a **recolour, not a fresh capture**: the run was in a
blue appearance, and its luminance was mapped onto the app's Parchment ramp.
Every stroke and all the layout are the app's; the exact colours are
approximated. Replace it when a real Parchment capture can be taken.

## Before announcing this anywhere

The App Store button has no destination yet. A live page advertising a download
that does not exist is worse than no page.
