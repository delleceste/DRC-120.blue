# DRC-120.blue — working notes for the 120 cm geometry

Forward notes for **this listening position only**: speakers 120 cm from the
front wall. This is the deployed geometry.

The project history through 2026-08-18 — every session, every retraction, and
the method as it was worked out — is **`../DRC-doc/NOTES.md`**. This file
starts where that one stops.

---

## 2026-08-18 — the repository split

The documents left `DRC-185` for a new repo, `../DRC-doc`, so that neither
geometry's measurement repo hosts the guides. Nothing moved out of *this*
repository; what changed is that 120 cm findings now get written **here**
rather than into the 185 cm repo's notebook, and that this repo finally has a
`CLAUDE.md`.

Corrected while moving: four references in the documents still pointed at
`txt/` and `new.filters.txts/`, renamed here on 2026-08-14.

---

## 2026-08-28 — two screens moved to the front wall

`120.blue.vs.2screens.front.wall/`: six sweeps in two sessions an hour apart.
`MPM.0` (14:32) is the standing layout; `SCREENS.FRONT.W` (15:40) has two GIK
screens taken off the back wall and the right-rear and stood on the front wall
near the L and R first-reflection points. Everything else unchanged.

**The MLP has moved.** 4.51 m from the front wall, not the 4.30 m still coded in
`../DRC-doc/roomgeom.py`. Recomputed for it, the front-wall reflection points are
**96.8 cm and 313.2 cm from the left wall, 117.1 cm above the floor**, excess delay
**6.67 ms**, geometric level −4.3 dB. (At 185 cm the same reflection arrived at
10.24 ms — this 4 ms is the depth cost the standing facts above refer to.)

### What the panels did

Energy in the 5.8–7.6 ms window, referenced to each measurement's own direct
sound, so a session level shift cannot fake it:

| octave | L | R | L+R | verdict |
|---|---:|---:|---:|---|
| 125–177 Hz | −0.01 | +0.15 | −0.12 | nothing, as a porous screen should |
| **355–710 Hz** | **−2.28** | **−1.89** | **−1.89** | **confirmed** |
| 710 Hz–1.4 kHz | −2.95 | −2.33 | −2.50 | spoiled, see below |
| 1.4–2.8 kHz | +1.05 | −1.31 | +0.19 | genuine null |
| 2.8–5.7 kHz | −1.41 | −1.17 | −4.70 | not repeatable |

The 355–710 Hz figure holds across every window from 6.2–7.2 ms out to 5.0–8.5 ms
(−1.87 to −2.05 dB) and the direct sound is unchanged (−0.06 / −0.68 / −0.52 dB).

**Above 1.4 kHz is a null, not a failure.** The reflection there already measures
17–21 dB below direct against −4.3 dB predicted for an omni source; that 13–17 dB
gap is the loudspeaker's rear directivity. There is nothing to absorb. No amount of
front-wall area, thickness or placement precision will change the band above
~1.4 kHz, so **do not buy front-wall treatment expecting to fix imaging up there** —
if the 120 cm depth deficit lives above 1.4 kHz its cause is the side wall at
2.06 ms or the ceiling at 3.06 ms, both earlier and louder.

Remaining headroom is 355 Hz–1.4 kHz only. The cheapest move is a **10–20 cm air
gap** behind the screens before adding any area; the 500 Hz first Fresnel zone spans
~2.2 m longitudinally and two 81.5 cm screens cover a fraction of it.

Cost of stripping the rear: late energy 20–80 ms moved by +0.14 / −0.19 / +0.65 dB.
Nothing measurable at the MLP.

### The error model, and why the repetitions were the wrong one

A metric that a 2 cm mic move destroys is describing interference detail no listener
experiences — two ears 17 cm apart and a moving head average through it. So the
error bar for any audibility claim is the **±8 cm L/R, ±10 cm F/B cloud**, not the
repetitions. Rebuilt on that basis, using the control window at 1.4–2.6 ms (floor and
near side wall, which front-wall panels cannot touch) as the drift detector:

| band | σ over the cloud, control window | observed between-session drift |
|---|---:|---:|
| **355–710 Hz** | **0.40 dB** (range 1.23) | **+0.04 dB** |
| 710 Hz–1.4 kHz | 1.39 dB | −3.13 dB |
| 1.4–2.8 kHz | 1.15 dB | +0.87 dB |

At 355–710 Hz the estimator is stable to 0.4 dB across ±8 cm and ±10 cm — head
movement genuinely does not disturb it — and the measured drift was 0.04 dB. The
−2.0 dB result is roughly **5σ against head movement**, a far stronger claim than the
~1 dB session floor supports.

Only 710 Hz–1.4 kHz is actually spoiled. Its control drift of −3.13 dB (−4.54 dB on L)
cannot come from the front wall; the likeliest cause is the left GIK panel being
nudged while the others were carried across the room. That octave alone needs redoing.

### Does it buy depth

In the one live octave the reflection went from −5.2 dB to −7.2 dB re direct (L+R) at
6.67 ms, from the same direction as the source. Detection threshold for a frontal
reflection at that delay is nearer −15 to −20 dB, so it was well above threshold
before and remains well above threshold after. Expect slightly firmer lower-midrange
image focus; do not expect a re-staging. The intervention is aimed correctly and is
under-dosed.

---

## Standing facts for this position

Settled, carried forward. Do not re-derive without a new measurement.

| | |
|---|---|
| why 120 cm | it puts the SBIR null at **71.5 Hz**. `L/6 = 123.3 cm` is the exact null of the 69.5 Hz mode, 3 cm away, so 120 cm keeps near-full 46 Hz coupling while sitting in a flat region |
| σ over 18–90 Hz | **4.41 dB** (Sep 2025) and **4.56 dB** (Apr 2026), against 8.80 dB at 185 cm. Seven months and two REW versions apart, the two 120 cm sessions agree |
| the cost | 120 cm costs depth — the first reflection arrives earlier *and* louder, crossing out of the "depth" window |
| below 80 Hz | correct **the sum**, not each channel. Correcting each channel toward a common target deepens the mono-sum null at 45–56 Hz. Above 80 Hz, per-channel |
| what that bought | predicted +2.31 dB at 40–62.5 Hz, delivered **+2.26**, with 100–225 Hz untouched to 0.01 dB |
| the current build | 8-cycle FDW, LF tail enabled, 80 Hz spliced construction. Declared as `rscreen-20260812` |
| measurements behind it | the 2026-08-10 16:21 Rscreen pair |

## Open threads

1. **The deployed pair fails the group-delay gate.** Measured 2026-08-18 on
   `FLX-trimmed-48k.wav` / `FRX-trimmed-48k.wav`: **+20.8 / +20.9 ms at
   20.1 Hz**, against a 10 ms threshold. `FLX` also fails the gated-tone tail
   at 79 Hz (114 ms against a 103 ms limit); `FRX` passes it.

   The sharpest-feature test now **passes** at Q 7.6 / 8.4, where the
   pre-LF-tail build failed at Q 73 — so the rebuild did what it was for. What
   is left sits at the very bottom edge of the corrected band, 20 Hz being the
   lower limit of the inversion itself.

   Before treating this as a defect, carry it through the clamp: the gate is a
   **build-quality** threshold, not an audibility verdict, and R8 of the guide
   holds the audibility figures. The question to answer is whether 20 ms at
   20 Hz is the filter or the band edge.

2. **The tweeter asymmetry.** The right channel runs ~2 dB down above 4 kHz
   since the 2025 tweeter replacement; the originals are still held. The
   near-field material is here in `on.axis.61cm.txts/` — including the old
   tweeters and the distortion sweeps — but the finding is about the
   *speakers*, not this geometry, so write the conclusion in
   `../DRC-doc/NOTES.md`.

3. **The multi-point set is half unusable.** `120.blue.screens.multimeas.txts/`
   holds centre, ±8 cm L/R, ±10 cm F/B and two repetitions, measured with the
   screens prolonged by two panels and two foam blocks behind them.

   **The R-channel arm of this set is defective — do not draw noise estimates
   from it.** `R …repetition` sits +4.83 dB from `R …screens` in the 5.8–7.6 ms
   window with the mic untouched, while `repetition.2` agrees to 0.03 dB. Worse,
   `R 120.b.s-L+8` and `R 120.b.s-B+10` have a categorically different early
   structure: a −7.7 dB peak near 1.7 ms that dominates the 0.58 ms peak present
   in every other measurement in the set. That is not a position gradient. The L
   channel is clean across all seven.

   This retracts the earlier instruction to use the repetitions as a ~1 dB session
   floor. Use the **L-channel cloud** (see 2026-08-28 above): σ = 0.40 dB at
   355–710 Hz, 1.39 dB at 710 Hz–1.4 kHz, 1.15 dB at 1.4–2.8 kHz, measured in the
   1.4–2.6 ms control window. Before this set can serve as anyone's error model
   the R channel needs re-measuring.

---

## 2026-08-31 — house curve back to a Harman shape; the 20 Hz LF-tail group delay

Worked on the `120.blue.multi.pt.mdat` set: 5-position cluster (`C`, ±20 cm
F/B/L/R), L and R separately, swept from **16.1 Hz**, X801 baked in via
`LX = L-SP × X801`. Two threads — the house curve, and the group-delay gate.

### House curve: scoop out, Harman in

The `Rscreen` build sounds thin. The cause is **not** too little correction — it
is the **C2 upper-bass scoop over-correcting**. Drawn at −1.74 dB
(`../DRC-doc/house-curve-C2.txt`), `min(target, meas)` delivers it near
**−2.9 dB** at 90–140 Hz (the guide's step-5 errata), and that gouge in the
voice/cello band is what reads as thin.

Reverted to a no-scoop **Harman / Olive** shape: ~+4–5 dB LF shelf, flat mids,
gentle −1 dB/oct treble tilt. New files in `../DRC-doc`:

- `house-curve-harman.txt` — +4 dB shelf (canonical)
- `house-curve-harman-fuller.txt` — **+5 dB shelf, this is the one in use**
- `housecurve.py` — extended with the `harman()` generator

Chose **+5**: canonical Harman is +4, but rooms and DRC defaults run +5–6, the
retired `120.blue` build was +6, and cut-only makes +5 vs +4 differ by <1 dB
below 30 Hz (the rest clamps).

**HF left flat on purpose** — the system is not bright here, if anything the
opposite. The Harman file carries the −1 dB/oct tilt so REW's target-level calc
sees the true shape, but **the filter is unity above 225 Hz so the tilt is not
delivered**. A treble tilt would need a separate broad high-shelf in the
BruteFIR chain — not wanted.

**Delivered, verified against the filter coefficients** (no measurement in the
loop): `FLX`/`FRX` cut the 65–182 Hz band **5.2 dB / 5.8 dB less** than Rscreen
(−6.5 dB → −1 dB). ≈ 4.3 dB of that is the target-shape change, the rest is
C2's scoop no longer over-delivering. The 90–160 Hz region moves from Rscreen's
**−3.1 dB to +3.3 dB** re midrange; deep-vs-upper balance goes room **−2.4 →
filtered −0.4**. Large, intended change in the warmth band; the seat gets most
of it (broadband room gain there, not a sharp mode).

### This build vs the recorded old deployment vs Rscreen

Time domain, 48 kHz, 131072 taps:

| | peak | pre-peak energy | worst GD excess 20–200 Hz |
|---|---|---|---|
| OLD `omdrc-801N/…/48000/L.raw` | 24002 | **67.6 %** | **+385 ms @ 29 Hz** |
| OLD `…/R.raw` | 24000 | 32 % | +72 ms @ 79 Hz |
| NEW `multi.pt/FLX-trimmed` | 8192 | 31.5 % | +22 ms @ 21 Hz |
| `Rscreen/FLX-trimmed` | 8193 | 43 % | +22 ms @ 20 Hz |

The recorded old deployment still carries the §5 pathology on L (+385 ms at
29 Hz, two-thirds of its energy before the peak — the 28.93 Hz notch inverted).
The new build is the cleanest of the three by a wide margin: ~17× less GD
excursion than old L, symmetric L/R.

Correction-wise: OLD = spiky high-Q modal cuts (−2 to −5 dB, hence the 385 ms).
Rscreen = deepest, the over-deep scoop (−6 to −10 dB at 80–160 Hz). NEW =
smooth broad trim, 0 to −3 dB, no narrow features. It is **marginal in
magnitude relative to the uncorrected sum** because the spatially-averaged room
here is only ~2 dB upper-bass heavy — 120 cm was chosen for being well-behaved.
The win over Rscreen is "the gouge is gone", not "more correction".

### The 20 Hz group-delay failure — the LF tail

`drc_acceptance.py` fails the 20–200 Hz group-delay gate: **+22 ms @ 21 Hz** on
both channels (Rscreen +20.8; the deployed pair too).

**Root cause: the minimum-phase LF-tail corner at 17 Hz, 24 dB/oct.** Sweeps
started at 16.1 Hz; REW places the corner at ~sweep-start + 1 Hz
([[rew-minphase-lf-tail-corner]]). A 4th-order high-pass has large group delay
just above its corner, and the correction-band edge sits only ~½ octave above
it, so the band-limited division inherits that phase. Measured: `F.common`
carries ~18–23 ms of GD excess at 20–21 Hz **while its magnitude is already
clamped to unity**; `Fper_L` contributes 1.6 ms. The tail enters **twice** in
this session's chain — once in the divisor `LR-SP-MP`, once in the
`Fl → L.Filter` minimum-phase copy (both "LF tail from 17 Hz at 24 dB/oct").

**Knob 2 — common-filter low edge 20 → 25 Hz** (`F.common` limits): helped,
27 → 22 ms, and it cleared the `FLX` gated-tone tails. Not enough to pass the
GD gate. Costs ~1 dB of taming at 20 Hz, which the fuller Harman target barely
asks for anyway. REW centres the one-octave blend *on* the limit (±½ oct), so a
25 Hz edge is ~75 % blended out at 21 Hz — hence the residual.

**Fixes, cheapest first:**

1. **LF-tail slope 24 → 12 dB/oct** in *both* minimum-phase steps (`*-MP` and
   `Fl → L.Filter`). Halves the GD near the corner. No re-measure. Try first.
   Costs nothing real — the gentler magnitude roll below 17 Hz only asks for
   more LF, and cut-only clamps it.
2. **Re-measure with sweeps from ~12 Hz** → corner ~13 Hz, a full octave below
   the band edge. Safety note below.
3. **Accept it.** +22 ms at 21 Hz is ~0.45 of a cycle, below LF group-delay
   audibility thresholds, and the deployed pair fails identically. Build-quality
   gate, not audibility (R8).

**Re-measuring — mic position:** 1–2 cm drift at centre is irrelevant. The
cluster spans ±20 cm on purpose; λ/4 at 80 Hz is ~1 m, so 1–2 cm in the
correction band is nothing, and it sits inside the ~1 dB session floor
(Trap #5). Keep speakers, gain, mic height and orientation fixed.

**Sweep from 10 Hz — is it dangerous for the speakers?** Mildly, and it is not
worth it. The N801 is a ported 15", tuned ~20–25 Hz; below tuning the cone
unloads and excursion rises steeply for constant drive. A log sweep dwells
equal time per octave, so 10–20 Hz gets as much time as 10–20 kHz — real
over-excursion risk at the −12 dBFS level used for this set. And it buys nothing
acoustically: there is no usable data below ~16 Hz, you only want REW to place
the tail corner lower. So **start at 12–14 Hz, not 10** (a ~13–15 Hz corner is
already a clean octave below a 25 Hz edge), drop the LF sweep level to
−18…−20 dBFS, run one trial sweep and watch the woofer — chuffing or visible
large excursion → raise the start / lower the level.

### X801 — what the crossover correction actually does

- **Magnitude: 0.00 dB flat 150 Hz–15 kHz.** Tonally transparent.
- **Excess phase** (best-fit pure delay removed): cuts total deviation ~**30 %**
  over 200 Hz–15 kHz (L 674° → 469° ptp, R 695° → 466°).
- **Concentrated at the woofer/midrange crossover, 200–700 Hz**: R excess-phase
  std 67° → 24°, L 201° → 152°; ≈ 1.3 ms group-delay flattening. This is the
  audibly worthwhile part — "precision in the lower midrange".
- **Above ~1 kHz** it straightens a gentle phase tilt (makes a wrapped-phase
  overlay look far flatter up top) but does **not** reduce the fast
  comb/diffraction ripple and does **not** correct the FST/tweeter crossover at
  3.5 kHz. That flattening ≈ a near-constant delay: perceptually mild.
- "More air in the highs" is most likely the **upper-bass unmasking** (90–160 Hz
  down ~5 dB vs Rscreen), not X801.

### TL;DR — rebuild the filter in REW

Divisors (`LX-MP`, `RX-MP`, `LR-SP-MP` = the spatial `SUM-MP`) and the
5-position cluster already exist in `120.blue.multi.pt.mdat`. Only the target
and two settings change.

1. **EQ → House Curve** → load `../DRC-doc/house-curve-harman-fuller.txt`.
   *(no scoop, +5 dB Harman shelf — replaces C2)*
2. **EQ → Set target level** → let REW calculate. Export as `Target LR.RMS`.
3. *(only if chasing the GD gate)* re-make `LX-MP` / `RX-MP` / `LR-SP-MP` with
   **LF tail 12 dB/oct**, not 24. *(halves group delay near the 17 Hz corner)*
4. **`F.common`** = Trace Arithmetic `A / B`, A = `Target LR.RMS`, B = `LR-SP-MP`,
   **Max gain 0.0 dB, limits 25–80 Hz**. *(25 not 20: keeps the LF-tail phase off the band edge)*
5. **`Fper_L`** = `A / B`, A = `Target LR.RMS`, B = `LX-MP`, **Max gain 0.0 dB,
   limits 80–225 Hz**. Repeat → `Fper_R` from `RX-MP`.
6. **`Fl`** = `F.common × Fper_L`.  **`Fr`** = `F.common × Fper_R`.
7. **`L.Filter`** = minimum-phase copy of `Fl` (**LF tail 12 dB/oct** if step 3
   was done). Same → `R.Filter` from `Fr`.
8. **`FLX`** = `X801 × L.Filter`.  **`FRX`** = `X801 × R.Filter`. *(bakes in the crossover all-pass)*
9. Trim → `FLX-trimmed` / `FRX-trimmed`. Export 48 kHz WAV. `REW2raw.sh` → `L.raw` / `R.raw`.
10. Verify: `cd ../DRC-doc && python3 drc_acceptance.py …/FLX-trimmed-48k.wav …/FRX-trimmed-48k.wav`.
    GD gate should pass; if not → `F.common` edge to 28 Hz, or re-measure from 12 Hz.
11. Sanity-check tonal result **below 200 Hz only** (single-point comb above
    that): overlay `LR.filtered` vs `L+R.orig`, both un-FDW'd *or* both FDW'd,
    Align SPL over 400 Hz–2 kHz.
