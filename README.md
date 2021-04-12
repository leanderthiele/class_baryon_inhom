# CLASS modifications for the Jedamzik & Pogosian three-zone model

Contains modified files to compute non-standard recombination histories
with a three-zone model for the baryon density.

Additional dependency: GNU scientific library (tested with v2.6)

Additional CLASS input file parameters for the three-zone model (all floating point numbers):
```
baryon_inhom_b
baryon_inhom_D1
baryon_inhom_f2
baryon_inhom_D2
```
These parameters completely specify the three-zone PDF.
Either all four or none must be set.
If none of these are set, standard recombination is computed.

The code uses a GSL non-linear solver to deduce the entire PDF.
The usual CLASS error handling is invoked if the specified constraints are inconsistent.

NOTE: for this to work, the default GSL error handler is turned off (since it would simply exit on error which
is inconvenient when running MCMC etc.). If you combine these modifications with other extensions
that rely on the GSL, this should be kept in mind.

In addition to the above four additional input parameters, the code also adds the string parameter
```
baryon_inhom_xe_file
```
If this parameter is set, the recombination history xe(z) is written to that file.
Note that, despite the name, this option can also be used if the three-zone model is not wanted
(i.e. for standard recombination histories).

Additionally, the modified code also allows a change in the 2s->1s transition rate,
using the input parameter (floating point)
```
L2s1s
```
which is in 1/sec (default: 8.2206).
This functionality is unrelated to the three-zone model and only included for historical reasons.

If any of the above options is set, it is required that recombination is computed with HyRec,
i.e. specify
```
recombination = hyrec
```
in the CLASS parameter file.

All modifications to the main branch CLASS code are marked with "LFT".
