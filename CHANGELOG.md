# Changelog

## v1.0.0 — Proton port

First release. A Linux/Proton port of the Crimson Desert RX 580 fix:

- Two patched vkd3d-proton DLLs (`d3d12.dll`, `d3d12core.dll`, x86_64) that
  make the game start and render on AMD Polaris (RX 470/480/570/580/590):
  forged feature-level reporting, per-stage FP16 handling, Polaris
  shader-compiler workarounds, and emulated GPU-driven command submission
  (correctness half; the multi-draw frame-rate collapse stays dormant in this
  build — its enabling flags are never set by any compile).
- Install without touching Proton: DLLs sit next to the game `.exe` and load
  on their own — no launch options, no overrides.
- Full debug info and working logging included (deliberately unstripped).
- Based on Vidith007's
  [RX-580-CRIMSON-DESERT-FIX](https://github.com/Vidith007/RX-580-CRIMSON-DESERT-FIX)
  v2.0.0 fix; the underlying vkd3d-proton patch is the same family. See
  `THIRD-PARTY-NOTICES.md` and `source/`.
