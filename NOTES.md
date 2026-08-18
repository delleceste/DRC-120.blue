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

3. **The multi-point set is unanalysed.** `120.blue.screens.multimeas.txts/`
   holds centre, ±8 cm L/R, ±10 cm F/B and two repetitions, measured with the
   screens prolonged by two panels and two foam blocks behind them. The
   repetitions are what set the ~1 dB session floor — use them as the noise
   estimate for any placement claim drawn from this set.
