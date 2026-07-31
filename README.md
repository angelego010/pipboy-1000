# PIP-BOY 1000 PROTOTYPE

**Live: https://angelego010.github.io/pipboy-1000/**

A build course. One file, no build step, no network calls.

```
index.html   the whole thing — course + journal + wiring sheet + holotape
fonts/       DotGothic16 + JetBrains Mono, local (same pair as the lab sheet)
_spec/       the six agent specs it was generated from; gitignored, not shipped
```

Works offline after first load. Everything he writes lives in `localStorage`
on that machine — nothing is uploaded, there is no account and no server that
could receive it.

## The holotape

Because there is no server, a new phone starts empty. Section 7 ejects the whole
page as one short code he pastes on the other device (or saves as a file).

It carries **decisions, not furniture**: the 25 seeded bin rows and their prose
are rebuilt from the file on load, so only the ones he has touched travel. A
fresh tape is ~170 characters, a well-used one ~500 — short enough to paste into
a message. Format `PB1000.1.<base64>.<checksum>`; the checksum exists because
the failure that actually happens is a code cut short by a chat app.

Loading replaces, never merges, and asks twice. Every rejection path says what
is wrong in a full sentence — a control that fails silently gets reported as
broken.

The same split runs in `load()`: a seeded row's words belong to the file, only
his decisions belong to the store, so a corrected line reaches someone who
already opened the page.

## What it is

A Pip-Boy, not a virtual pet. It borrows Guadalupe's *shape* — small screen,
three buttons, one board — because that shape is proven, cheap and finishable.
What goes on the screen is Gabe's.

Nine stages, from a Pi in a padded envelope to a screen he designed that
survives a power cut. **Zero solder joints by design** — he has soldered once,
in a free period; an iron in the cart invites inventing a reason to use it.

## The three lines

**The frame** is closed: one Pi, one screen, three buttons · a menu those
buttons drive · one value that ticks on its own · state that survives the pull.
Four rows, and the fifth is capped.

**The line** sorts every idea into free or not-free. Almost everything iconic on
a Pip-Boy is pixels and costs nothing — RADS, S.P.E.C.I.A.L., caps, quest log,
Vault Boy, a drawn map. A real Geiger tube is a new part. Pixels are his today;
new parts are dated, not refused.

**The bin** holds everything else with a date on it. Twenty-five ideas
pre-seeded, fourteen above the line and eleven below.

## Gabe-proofing

Stage N+1 opens when stage N is marked done **and** its dwell has elapsed
**and** it has a journal entry. A locked stage names which of the three is
missing, counts the dwell down live, and links back to the stage he is actually
on — because last time a by-design lock got reported as "not working".

Skip-proof, **not tamper-proof**. The console is right there and that is fine.
No obfuscation was added and none should be.

Controls lock via the `.disabled` property, never `setAttribute('disabled', …)`
— that trap ate a day on IR/UV.

## Two things a human decides

1. **Length.** Body prose is ~5,800 words after an 18% cut. Going lower means
   deleting a reference table (PARTS, DO NOT BUY, the SETUP table, the PIN
   TABLE) — holes and order, the part that is supposed to survive. Left long
   on purpose. Cut a table or accept it.
2. **Nothing is hosted.** Same call as the free-period lab. It could go to
   `angelego010.github.io` if Gabe wants it on his phone at the bench.

## The parts call

A second-hand **Pi 3B+**, not a Zero 2 W: the header is already soldered, no
mini-HDMI or USB-OTG adapters, and the tutorials all apply. **MSP2807** 2.8"
ILI9341 on hardware SPI0 — rated 3.3–5 V, run at 3.3. Buttons on BCM 16/20/21
with internal pull-ups, active-low: the same circuit he already built in the
free period, said out loud on the sheet.

Header pins 2 and 4 are the loudest rule on the page and stay absolutely
forbidden, even though the documented screen would tolerate 5 V.

## Verified

Renders at 1400 and 390 wide, no body overflow. Locked vs unlocked survives
greyscale (solid vs dashed, never hue). The wiring figure survives greyscale
because every wire carries its physical pin number. Pinout checked against
Raspberry Pi docs and the LCDwiki MSP2807 manual. Page script parses clean.
