# 2026-08-12 build — archived before the LF-tail fix

Snapshot taken 2026-08-12, immediately before rebuilding the minimum-phase
copies with **LF tail enabled**. Everything here was produced with
`No LF tail`, which corrupts magnitude at low frequency.

## Why this is archived, not deleted

Every minimum-phase copy in this build fails the one property a minimum-phase
copy must have — **it must leave |H| unchanged**. Max |error| in dB:

| conversion | 5–15 Hz | 15–25 Hz | 25–40 Hz | 40–225 Hz |
|---|---|---|---|---|
| `LX` → `LX-MP` | **13.41** | 0.58 | 0.03 | 0.33 |
| `RX` → `RX-MP` | **8.88** | 0.53 | 0.03 | 0.04 |
| `SUM` → `SUM-MP` | **11.15** | 0.56 | 0.02 | 0.03 |
| `FL` → `LFilter` | 0.21 | **2.41** | 0.30 | 0.13 |
| `FR` → `RFilter` | 0.21 | **2.41** | 0.30 | 0.06 |

In the exported WAVs this shows as a **−11.4 dB notch at 19.96 Hz**, identical
in FLX and FRX to 0.01 dB — deterministic processing, not acoustics. It is
0.23 Hz wide at −6 dB, so REW's own 0.366 Hz display grid cannot resolve it and
shows only a −4 dB dip. It is what fails the R8 narrowest-feature and
group-delay tests, both of which land at ~20 Hz.

HF is clean (0.000–0.002 dB above 1 kHz): the traces already run to 24 kHz =
Nyquist, so there is no top-end truncation edge. **HF tail is not needed.**

## What is otherwise good about this build

This is the first build using the §11 construction — common correction below
80 Hz, per-channel above — and that part worked as predicted:

| band | before | old per-channel build | this build | gain |
|---|---|---|---|---|
| 20–40 | +7.20 | +5.15 | +5.85 | +0.71 |
| **40–62.5** | +1.78 | **−0.72** | **+1.55** | **+2.26** |
| 62.5–100 | +7.02 | +1.27 | +1.99 | +0.72 |
| 100–160 | +9.41 | +0.86 | +0.86 | +0.01 |
| 160–225 | +6.12 | +3.41 | +3.42 | +0.01 |

Predicted +2.31 dB at 40–62.5 Hz, delivered +2.26, with the 100–225 Hz
correction untouched to 0.01 dB. The 80 Hz splice was verified: the two
band-limit ramps sum to 0.995–0.998 across 57–113 Hz, and the worst case where
`FL` cuts deeper than either candidate correction alone is 0.00 dB.

The target is **not** affected — it was built from `LX`/`RX`, which never went
through the minimum-phase step, so `LRrms+phavg` and `Target LRrms+phavg` here
are sound and were carried forward unchanged.

## Contents

| file | what it is |
|---|---|
| `FLX-48k.wav`, `FRX-48k.wav` | the 2026-08-12 deliverables (spliced build, no LF tail) |
| `FLX.diff-48k.wav`, `FRX.diff-48k.wav` | the 2026-08-11 differential build, for comparison |
| `new.filters.txts/` | all 41 exports; `*.diff.txt` are the 08-11 chain |
| `120.blue.Rscreen.mdat` | the REW session as it stood |

Underlying measurements are the 2026-08-10 16:21 `Rscreen` pair, unchanged.
