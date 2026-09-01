# Working notes for this repository

**DRC-120.blue** — the lab for the **120 cm** geometry: B&W **Nautilus 801**
(aluminium dome, *not* the Diamond series) 120 cm from the front wall, in a
1905 house, ~58 m³. This is the **deployed** geometry — what is in service is
built from the measurements here.

Measurements in REW, filters convolved by BruteFIR. This repo holds REW
sessions, their text exports, and the filter WAVs. **No documents** — those are
in `../DRC-doc`.

## The four repositories

| repo | role |
|---|---|
| **DRC-120.blue** (here) | the lab: REW exports and filter WAVs for the 120 cm geometry |
| **../DRC-doc** | the guides, the studies, the tooling. `REW-INVERSION.md` is the procedure; its worked example is *this* geometry |
| **../DRC-185** | the 185 cm geometry, its own measurement set |
| **../../open-media-drc** | the product: deployed coefficients, versioned by **release tag** |

`../DRC-120` (no `.blue`) is **retired — never use it.** Several early
conclusions were derived from it and had to be re-derived; anything citing it
is suspect. Older archives: `../803D2/`, `../803D2/2017-subs/`,
`../801N.first.measurements/`.

## Sessions and their exports

Each `.mdat` is a REW session; each `.txts/` directory is its unsmoothed text
export. They pair by name.

| session | exports | what it is |
|---|---|---|
| `120.blue.mdat` | `120.blue.txts/` | **the legacy inversion work — this is what is deployed.** `L.120.Blue`, `R.120.Blue`, the `LX`/`RX`/`-MP`/`FLX`/`FRX` chain, `X801 (revised)` |
| `120.blue.Rscreen.mdat` (+`…12.cycles` variant) | `120.blue.Rscreen.txts/` | the **2026-08-10 Rscreen pair** and the `rscreen-20260812` build. Never deployed |
| `120.blue.multi.pt.mdat` | `120.blue.multi.pt.txts/` | the **2026-08-31 five-position Harman rebuild**: `C` + ±20 cm F/B/L/R, `F.common`/`Fper_L`/`Fper_R`, `LR-SP-MP`. Never deployed |
| `120.blue.screens.multimeas.mdat` | `120.blue.screens.multimeas.txts/` | multi-point: centre, ±8 cm L/R, ±10 cm F/B, plus two repetitions. **R arm defective** — see `NOTES.md` |
| `120.blue.vs.2screens.front.wall.mdat` | `120.blue.vs.2screens.front.wall/` | 2026-08-28 front-wall screen A/B, `MPM.0` vs `SCREENS.FRONT.W` |
| `on-axis.61cm.mdat` | `on.axis.61cm.txts/` | near-field tweeter comparison, including the **old** tweeters and distortion sweeps. Exports start above ~500 Hz |
| `foam.screens.opendoor.mdat`, `meas.120.blue.2026.04.18-dac8stereo+fosiV3-mono.mdat`, `meas@120.blue.mdat` | — | treatment and chain variants |
| `comparisons/*.mdat` | — | 2026-08-31 side-by-side of legacy / Rscreen / multi-point results |

Loose CSVs at the root (`LEFT-measured.csv`, `RIGHT-measured.csv`,
`L+R-NO_DRC.csv`, …) are Sep-2025 and Apr-2026 exports that predate the
`.txts/` convention.

### The renames

| old | now | when |
|---|---|---|
| `txt/` | `120.blue-with-inversion.txts/` | 2026-08-14 |
| `new.filters.txts/` | `120.blue.Rscreen.txts/` | 2026-08-14 |
| `120.blue-with-inversion.txts/` | **`120.blue.txts/`** | 2026-09-01 |
| `120-blue-with-inversion.mdat` | **`120.blue.mdat`** | 2026-09-01 |

If you meet `txt/`, `new.filters.txts/` or anything `…with-inversion…`
anywhere, it is stale.

**`120.blue.mdat` is not byte-identical to the session it replaces.** It was
also *cleaned* of measurements made by other techniques, and re-exported. The
audited original — SHA-256
`b184b824236868a898c33877a56d0f1003a2e442922d8b4f9c05ef1a51b8d6c7`,
57 685 240 B, the file named in `open-media-drc`'s
`doc/FILTER_PROVENANCE_AND_RESPONSE.md` — is recoverable as
`git show 23b1a6a:120-blue-with-inversion.mdat`. The current file hashes
`62d534dac28abdd697223dde9187f02c78c1aa10f073cb51bfc5a6667efc953c`.

Two things survived the clean unchanged, verified 2026-09-01: `FLX`, `FRX`,
`FLX-trimmed`, `FRX-trimmed` and `X801 (revised)` re-export **numerically
identical** to the pre-rename exports (0.00e+00 over all 65533 rows), and
`120.blue.txts/FLX-trimmed-48k.wav` still matches the deployed `L.raw`. What
did change for the better: the measurement and `-MP` traces were previously
exported at **96 ppo, Psychoacoustic smoothing** (1160/1385 rows) — the
estimator §9 of the guide forbids near an inversion — and are now unsmoothed
full-resolution (60198/65533 rows). `X801.txt` (as distinct from
`X801 (revised).txt`) and the `+2dB` variants are not in the new export.

## Traps

1. **`LEFT+RIGHT-measured.csv` is not a 120 cm measurement.** Its header says
   `* Measurement: L+R.137.Blue` — it is a **137 cm** sweep, while its
   same-session siblings `LEFT-measured.csv` and `RIGHT-measured.csv` really
   are `L.120.Blue` / `R.120.Blue`. The genuine Sep-2025 120 cm sum is the
   *complex sum of those two*, not this file. It is a useful extra placement
   point, not a duplicate of 120 cm.
2. **`FLX`/`FRX` are not plain exports of the inverse filter.**
   `FLX = X801 (revised) × LFilter` — the crossover all-pass is **baked into**
   the deployed filter, so `FLX` is *not* minimum phase. Any argument that
   assumes it is, is wrong.
3. **Never re-export `X801.rephase`.** It is verified good and one field in it
   is deliberately unset. Rebuilding it silently changes the crossover
   correction that every deployed filter carries.
4. **`archive/2026-08-12-noLFtail/` is a counter-example, not a spare.** Every
   minimum-phase copy in it was built with *No LF tail* and fails the one
   property such a copy must have — leaving |H| unchanged (13.4 dB error at
   5–15 Hz, a −11.4 dB notch at 19.96 Hz). Kept to show the failure. Do not
   read data from it. Its measured traces match the live ones to 0.000 dB; only
   the target differs, by +0.03 dB.
5. **Window metrics have a ~1 dB session floor.** Two measurements of the same
   configuration in different sessions differ by about that much, so a panel or
   placement change under ~1 dB is not evidence of anything.

## Naming and versioning

- **Stable names for the current build**: `FLX-48k.wav`, `FLX-trimmed-48k.wav`
  (and `FRX`). These always mean *what is current*.
- **Suffix only while two builds must coexist** for comparison (`FLX8` vs
  `FLX`, `FLX.diff`), then collapse to the stable name once one wins.
- `*-1.5.4-*.wav` are **pinned copies of a release**, tracked so they travel
  between machines. They are not a build.
- **Deployments are versioned by `open-media-drc` release tags**, not by
  filenames and not by this repo. That repo answers "what was in service".

> **"Current" in this repo does not mean "in service."** Verified 2026-09-01:
> `/usr/local/etc/open-media-drc/filters/120.blue/48000/L.raw` and `R.raw` are
> the exact float64 promotion of the int32 PCM in `FLX-trimmed-1.5.4-48k.wav`
> and `FRX-trimmed-1.5.4-48k.wav` — bit-for-bit, all 131072 samples — i.e. the
> **legacy `120.blue.mdat` build** (peak at sample 24002/24000). The root
> `FLX-trimmed-48k.wav` (Rscreen) and `120.blue.multi.pt.txts/` builds are
> uncorrelated with what runs. Neither has ever been deployed at 48 kHz.

### The design declaration

`omdrc-designs/120.blue/rscreen-20260812/design.json` is the attestation that
ties this repo's exports to a deployment: SHA-256 of every input measurement,
every filter export, the filter WAVs and the corrected exports, plus the
alignment actually detected (8192-sample delay, −3.0003 dB txt→wav gain). The
matching runtime config is `open-media-drc`'s
`configs/120.blue/brutefir-<rate>@rscreen-20260812.conf`; at runtime the
coefficients live in `filters/<geometry>/` under `${PREFIX}/etc/open-media-drc`.
`scripts/REW2raw.sh` converts REW WAV → raw `FLOAT64_LE` with an
`input_rate/target_rate` coefficient scale.

If you rebuild the filters, the design id changes and a new `design.json` is
declared. Do not edit an existing one.

## Verifying a filter

The tool is next door:

```sh
cd ../DRC-doc && python3 drc_acceptance.py \
    ../DRC-120.blue/FLX-trimmed-48k.wav ../DRC-120.blue/FRX-trimmed-48k.wav
```

Three tests: sharpest feature (**Q ≤ 12** — not FFT bins, whose spacing is
`fs/n` and so depends on file length), group-delay excursion (10 ms, 20–200 Hz)
and gated-tone tails (median over nine tone lengths). `X801.wav` is the
known-good control and passes all three.

**The thresholds are a build-quality gate, not a verdict on audibility.** R8 of
`../DRC-doc/REW-INVERSION.md` carries the audibility figures separately — which
matters here, because the current pair does not pass. Measured 2026-08-18:

| | sharpest feature | group delay | gated tails |
|---|---|---|---|
| `FLX-trimmed-48k.wav` | PASS Q 7.6 | **FAIL +20.8 ms @ 20.1 Hz** | **FAIL 114 ms @ 79 Hz** |
| `FRX-trimmed-48k.wav` | PASS Q 8.4 | **FAIL +20.9 ms @ 20.1 Hz** | PASS |

The Q test is the one the 8-cycle FDW and LF-tail rebuild was meant to fix, and
it did — it used to fail at Q 73. The group-delay failure sits at the very
bottom of the corrected band. See `NOTES.md`.

## Where to write things down

- A finding about **this geometry** → `NOTES.md` here.
- A finding about the **method**, the room, or the tools → `../DRC-doc/NOTES.md`.
- A finding about the **185 cm** position → `../DRC-185/NOTES.md`.

The project history through 2026-08-18, including every retraction, is
`../DRC-doc/NOTES.md`. Do not restate it here.

## A habit worth keeping

Several conclusions this project reached were wrong on first pass and were
caught by carrying a number through to the thing that actually ships. Before
acting on a discrepancy in a divisor, a measurement or a metric, **carry it
through `min(Target − divisor, 0)` and see whether it survives the clamp.** It
usually does not.
