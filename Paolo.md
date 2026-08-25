# Paolo: bass cancellation, Dirac Live, and common correction

## Executive conclusion

Paolo's measurements contain two different low-frequency problems:

1. At approximately **34–41 Hz**, the left and right speakers produce useful
   output individually but oppose one another at the listening position. This
   is principally an **L/R phase-cancellation problem**.
2. At approximately **47–50 Hz**, both individual speaker-to-microphone
   responses are low, while left and right are nearly in phase with one
   another. This is a **common acoustic-transfer deficit**, not an indication
   that the B&W 804 Diamond D2 is intrinsically weak.

The second feature can respond to magnitude correction if its measured
transfer function is finite and substantially minimum phase. Geometry does
not automatically mean excess phase. A room- or placement-created feature can
still be minimum phase and invertible. Conversely, magnitude boost cannot
repair a true zero or a non-minimum-phase cancellation; it can only increase
the small residual pressure at the measurement location, with potentially
large headroom and excursion costs.

Dirac produced a materially flatter measured bass response, mainly through
magnitude-envelope reshaping around 44–52 Hz. It did not remove the L/R
cancellation: the worst cancellation moved from about 37.4 Hz to about
40.6 Hz. The available final acoustic responses prove that the relative phase
changed, but they do not reveal Dirac's exact filter, its absolute electrical
boost, or whether it used an explicit parametric all-pass section.

The common-filter method documented in `../DRC-doc/REW-INVERSION.md` remains
useful as a **summation-safety rule** below 80 Hz. It prevents independent L/R
correction from making a mono cancellation worse. A cut-only common filter
cannot fill either of Paolo's deep deficits.

## 1. Identification of the exported measurements

The best-supported interpretation of the exported files is:

| files | time on 20 November 2024 | interpretation |
|---|---:|---|
| `L nov 20.txt`, `R nov 20.txt`, `L+R nov 20.txt` | 20:43–20:44 | main speakers only, Dirac Live active |
| `L NODRC nov 20.txt`, `R NODRC nov 20.txt`, `L+R NODRC nov 20.txt` | 20:52–20:53 | main speakers only, Dirac disabled |

`L_Paolo.txt`, `R_Paolo.txt`, and `LR_Paolo.txt` are effectively duplicate
exports of the first triplet, apart from approximately 0.01 dB/export-text
differences.

All six direct measurements used the left speaker as the acoustic timing
reference. The calculated complex L+R response agrees with the physical L+R
sweep to a median absolute error of approximately **0.23 dB** for NODRC and
**0.19 dB** for Dirac over 20–300 Hz. The timing and phase are therefore
coherent enough to study L/R summation.

The headers themselves do not record `Dirac` or `subwoofer`. The classification
above also relies on the measurement history: Dirac was measured first, NODRC
was measured next, and subwoofers were introduced later. No separately
identified subwoofer text export is present in the current Paolo directory.

## 2. A flat loudspeaker can still measure with a geometrical dip

The free-field or anechoic response of a loudspeaker is not the same thing as
its response at a seat in a room. At one frequency and microphone position,
the measured pressure can be represented as

\[
P(f,r)=S(f)\,H_{room}(f,r)\,X(f),
\]

where:

- `S` is the loudspeaker's own response;
- `H_room` is the propagation, boundaries, modes, reflections, placement and
  listener-position transfer function;
- `X` is the electrical input.

The B&W can have a flat `S(f)` while `H_room(f,r)` has a deep depression.
That says nothing adverse about the intrinsic capability of the loudspeaker.

### How boost can apparently fill a geometrical dip

Suppose the direct contribution at the microphone is `1` and a delayed or
modal contribution is `-0.8`. Their residual is

\[
1-0.8=0.2,
\]

which is approximately −14 dB. If the input is multiplied by five, both
contributions scale:

\[
5-4=1.
\]

The microphone now reads the desired pressure, even though the geometrical
cancellation ratio remains exactly the same. The correction has not removed
the reflection or node; it has driven much more acoustic energy into the room
to enlarge the finite residual.

For an exact cancellation,

\[
1-1=0,
\]

and no finite common gain works:

\[
C(1-1)=0.
\]

Real measured notches are seldom mathematical zeros. Losses, unequal path
amplitudes, multiple reflections, microphone position and frequency smoothing
usually leave a finite residual. That residual can be raised at one location,
but often at a high cost and with excessive output elsewhere in the room.

### Minimum phase is the decisive distinction

A feature caused by room geometry is not necessarily an excess-phase feature.
After removing bulk propagation delay:

- If the local transfer is **minimum phase**, its magnitude and phase are
  linked. A finite dip can in principle be corrected by a causal stable
  magnitude inverse, including the phase change naturally associated with
  that inverse.
- If the feature contains substantial **excess phase**, ordinary magnitude EQ
  does not repair the timing behaviour. A mixed-phase FIR may approximate the
  part judged common and safe to correct, while a causal all-pass can re-time
  one source relative to another. These are not generally an exact causal
  inverse of the room's excess phase: the exact inverse of a stable all-pass
  is anti-causal or unstable.
- If the transfer has a non-minimum-phase zero or a true cancellation zero, an
  exact stable causal inverse does not exist. Trying to approximate it can
  require excessive gain, long filters, pre-ringing, or correction that works
  only at one point.

A simple delayed reflection can itself be minimum phase when the reflected
path is weaker than the direct path, despite producing a geometrical comb
filter. Thus neither the word `geometry` nor the presence of a dip establishes
the phase class.

The Paolo text measurements contain magnitude and phase, but the observed
before/after improvement alone does **not** prove that the 47–50 Hz feature is
minimum phase. That classification should be made by comparing each properly
windowed measured impulse response with its minimum-phase reconstruction and
examining the excess group delay, then repeating the test across microphone
positions.

## 3. Anatomy of the NODRC bass response

### 3.1 The 34–41 Hz L/R cancellation

The calculated cancellation region extends approximately from 33.7 to
39.9 Hz. The maximum cancellation loss is about **21.6 dB at 37.4 Hz**, with
left and right levels matched to within roughly 1 dB.

Using 1/6-octave views normalized to the respective midrange levels, at
37.4 Hz:

| response | relative level |
|---|---:|
| left | −5.6 dB |
| right | −7.1 dB |
| measured L+R | −18.0 dB |

The individual speakers are not severely deficient there. The large extra
loss appears when they are played together. Their raw phase separation is
approximately 173°, so the problem is dominated by L/R timing and phase.

### 3.2 The 47–50 Hz common transfer deficit

At approximately 47.6 Hz:

| response | relative level |
|---|---:|
| left | −18.4 dB |
| right | −12.8 dB |
| measured L+R | −19.0 dB |

The left/right phase separation there is only about **15°**, corresponding to
roughly **0.1 dB** of L/R summation loss. Therefore, left and right are not
cancelling each other at that frequency. Each individual speaker-to-seat
transfer is already low.

This does not identify the physical cause. Possibilities include a modal
pressure minimum, SBIR or another shared placement/listening-position effect.
Paolo's room dimensions and exact speaker/listener distances would be needed
to test those hypotheses. Anechoic or close-microphone data would separate the
loudspeaker response from the room response.

## 4. What Dirac changed

For the physical L+R response over 20–80 Hz, using 1/6-octave smoothing and
normalizing each measurement to its own midrange reference:

| metric | NODRC | Dirac | change |
|---|---:|---:|---:|
| deepest dip | −19.0 dB | −11.8 dB | +7.2 dB |
| peak-to-peak variation | 27.5 dB | 17.7 dB | −9.8 dB |
| RMS error relative to flat | 10.1 dB | 6.35 dB | −37% |

That is a real and substantial measured improvement. It did not, however,
come primarily from repairing L/R cancellation.

After removing the approximately 7.5 dB overall level difference between the
two measurement sessions, the corrected-minus-NODRC change decomposes as:

| band | magnitude/envelope contribution | phase/cancellation contribution | net sum change |
|---|---:|---:|---:|
| 34–40 Hz | +5.1 dB | +1.9 dB | +7.1 dB |
| 40–44 Hz | +6.5 dB | **−8.0 dB** | −1.5 dB |
| 44–52 Hz | **+9.4 dB** | −0.4 dB | +9.1 dB |

Around 44–52 Hz, nearly all the recovery is attributable to magnitude-envelope
reshaping. Dirac either applied relative bass gain, attenuated other
frequencies and allowed subsequent level restoration, or used a combination
of both. Final acoustic measurements cannot distinguish those internal gain
choices.

The result does not demonstrate that Dirac overcame the room geometry. It
shows that it increased the measured residual or lowered the surrounding
response enough to make the calibration region flatter.

### Headroom interpretation

At equal restored midrange playback level, +9.4 dB of relative correction is
equivalent to about 3 times the voltage and nearly 9 times the electrical power
at those frequencies. The unsmoothed pointwise acoustic-envelope change near
47.6 Hz reaches approximately +14.8 dB, although that number must not be
mistaken for a directly measured Dirac filter gain.

Such correction can consume amplifier headroom and woofer excursion. It may
also create excess bass at nearby seats where the geometrical depression is
shallower or absent. This is why spatial repeatability and output capability
must be checked before accepting a deep inverse.

## 5. Did Dirac use an all-pass filter?

Dirac Live is documented as a **mixed-phase** correction system. It corrects
magnitude and the excess-phase behaviour that its spatial model considers
common enough to correct safely. Any mixed-phase correction can be discussed
as containing a minimum-phase magnitude component and an all-pass-like phase
component, but that does not prove that Dirac inserted a specific parametric
all-pass at 40 Hz.

Dirac's technical overview distinguishes ordinary Dirac Live from Bass
Control: Bass Control explicitly makes extensive use of all-pass filters when
optimizing interacting bass sources. See [Dirac Live: a technical
overview](https://www.dirac.com/wp-content/uploads/2025/07/Dirac-Live-Whitepaper.pdf).

The Paolo measurements demonstrate a large change in final relative phase:

| state | worst L/R cancellation |
|---|---:|
| NODRC | 21.6 dB at 37.4 Hz |
| Dirac | 22.6 dB at 40.6 Hz |

Thus phase changed, assuming the acoustic configuration remained fixed. But
the cancellation was displaced rather than eliminated. The final acoustic
responses cannot reveal whether this resulted from an explicit all-pass,
Dirac's general mixed-phase FIR correction, channel delay, or the phase that
naturally accompanies its magnitude correction.

An electrical loopback with Dirac on and off, or the actual exported Dirac
filter impulses, would be required to identify the correction topology and
measure its pre-ringing or group delay separately from the room.

## 6. The common-filter technique below 80 Hz

Let the same correction `C(f)` be applied to both speakers:

\[
L'(f)+R'(f)=C(f)L(f)+C(f)R(f)=C(f)[L(f)+R(f)].
\]

The common filter cannot alter the left/right amplitude ratio or their phase
difference. Therefore:

- it cannot remove the 34–41 Hz L/R cancellation;
- a common boost can raise only the finite residual, without changing the
  cancellation depth relative to the individual contributions;
- the cut-only common filter specified in `REW-INVERSION.md` cannot add any
  absolute output to a dip;
- it does prevent independent channel filters from equalizing two nearly
  opposite contributors and accidentally making their cancellation deeper.

On Paolo's NODRC data, illustrative independent cut-only correction would
lose roughly **2–4 dB** of mono-sum output at several bass frequencies compared
with a genuinely common filter. This makes the common construction useful,
but as a protection mechanism rather than a null-filling mechanism.

## 7. Stereo DAC and later subwoofer integration

With one composite output per side, Dirac sees only:

\[
Left_{system}=Main_L+Sub_L,
\]

\[
Right_{system}=Main_R+Sub_R.
\]

It can correct each composite stereo channel, but it cannot independently
change main/sub delay, phase, polarity, level or crossover unless those
controls are provided elsewhere in the analogue or subwoofer path. Manual
main/sub alignment must therefore occur before Dirac measures the composite
channels.

A processor with independently addressable main and sub outputs can first
align the sources so that their acoustic contributions add rather than fight.
That can recover output through phase alignment instead of large magnitude
boost, conserving headroom. The possible improvement cannot be quantified
from the present text exports because they do not include time-referenced
main-only, sub-only and main+sub measurements for each side at an unchanged
microphone position.

This architecture issue is secondary to the mains-only result analysed above.

## 8. What should be measured next

To determine whether the 47–50 Hz depression is safely invertible and what
Dirac actually did:

1. Repeat NODRC left, right and physical L+R sweeps with the microphone and
   playback gain unchanged.
2. Repeat them at several nearby positions, preserving the acoustic timing
   reference.
3. Compare each windowed impulse response with its minimum-phase
   reconstruction and plot excess group delay through 20–100 Hz.
4. Repeat the sweeps with Dirac enabled at exactly the same output reference.
5. Capture an electrical loopback or export Dirac's filter impulses. Their
   transfer functions directly reveal magnitude gain, phase correction,
   latency and ringing.
6. If subs are evaluated, capture main-only, sub-only and main+sub on each
   side before any combined correction.
7. Verify maximum safe SPL, amplifier headroom and woofer excursion with the
   proposed correction active.

## 9. Final assessment

The B&W 804 Diamond D2 was not shown to be intrinsically weak. Paolo's NODRC
measurements show that the acoustic transfer from each loudspeaker to the seat
is low around 47–50 Hz, while a separate L/R cancellation dominates around
37–41 Hz.

Dirac can flatten a finite, sufficiently minimum-phase geometrical depression
because an inverse raises the remaining pressure at the calibration region.
That does not remove its physical cause. If the feature is excess phase,
non-minimum phase, position-dependent or a true zero, magnitude inversion is
incomplete, inefficient or unsafe.

The measured Dirac improvement came mainly from magnitude reshaping. Its phase
processing did not solve the most important L/R timing problem. For Paolo,
the correct hierarchy is therefore:

1. classify the 47–50 Hz feature as minimum phase or excess phase across
   positions;
2. correct placement and relative source timing where possible;
3. use a common sub-80 Hz correction to protect mono summation;
4. apply only the amount of inverse magnitude correction justified by spatial
   consistency, headroom and decay tests;
5. verify the result with physical L+R sweeps, not just separate-channel
   magnitude averages.
