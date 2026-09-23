# Third-party notices

This repository distributes compiled binaries that are **not** the repository
author's work and are **not** covered by the repository's Apache-2.0 licence.
This file records who owns what, under which terms, and where to get the
corresponding source.

If you only want to know one thing: **`fix/d3d12core.dll` and `fix/d3d12.dll`
are modified LGPL-2.1-or-later binaries, and their modified source is in
`source/RX580-proton-build.patch`.**

---

## Summary

| Component | In this repo | Licence | Modified? |
|---|---|---|---|
| The Proton port, packaging and docs | `README.md`, `INSTALL.md`, `fix/` layout | Apache-2.0 | Original work |
| The underlying game fix | Vidith007 / RX-580-CRIMSON-DESERT-FIX (Windows) | Apache-2.0 | Used as reference, see below |
| **vkd3d-proton 3.0.1** | `fix/d3d12core.dll`, `fix/d3d12.dll` | **LGPL-2.1-or-later** | **Yes** — see below |
| **dxil-spirv** | vendored inside `d3d12core.dll` | MIT | No |
| SPIRV-Headers, Vulkan-Headers | vendored inside `d3d12core.dll` | Apache-2.0 / MIT | No — byte-clean |
| Crimson Desert | **not distributed** | Pearl Abyss | No file modified |

Apache-2.0 does not and cannot cover the vkd3d-proton binaries. You cannot
relicense someone else's LGPL work by putting an Apache licence in the
repository root.

---

## vkd3d-proton — LGPL-2.1-or-later, modified

**Upstream:** https://github.com/HansKristian-Work/vkd3d-proton
**Version:** v3.0.1
**Licence text:** [`fix/licenses/vkd3d-proton-LICENSE.txt`](fix/licenses/vkd3d-proton-LICENSE.txt)
and [`fix/licenses/vkd3d-proton-COPYING.txt`](fix/licenses/vkd3d-proton-COPYING.txt), unedited.
**Authors:** [`fix/licenses/vkd3d-proton-AUTHORS.txt`](fix/licenses/vkd3d-proton-AUTHORS.txt), unedited.

`fix/d3d12core.dll` is a **modified** build. LGPL-2.1 sections 4 and 6 require
the corresponding modified source to accompany the binary. It does:

> [`source/RX580-proton-build.patch`](source/RX580-proton-build.patch)

To reproduce the build, clone upstream at tag `v3.0.1`, then:

```bash
patch -p1 < RX580-proton-build.patch
```

The bulk of that patch is the Polaris / Crimson Desert fix published by
[Vidith007](https://github.com/Vidith007/RX-580-CRIMSON-DESERT-FIX) (see his
`source/vkd3d-proton-3.0.1-rx580-polaris.patch`, same upstream base);
this port keeps it and adapts the result for Proton on Linux.

---

## dxil-spirv — MIT

Vendored inside `d3d12core.dll`, pristine submodule state.
**Copyright:** "Copyright (c) 2019-2022 Hans-Kristian Arntzen for Valve Corporation"
**Licence text:** [`fix/licenses/dxil-spirv-LICENSE.txt`](fix/licenses/dxil-spirv-LICENSE.txt)

---

## What is not distributed here

**No Crimson Desert file is modified or redistributed.** Pearl Abyss made the
game. This package contains none of it. The fix works by placing two DLLs next
to the game's executable and telling Proton to prefer them, which is why
uninstalling is just deleting two files.

**No Proton, Wine, driver, or system file is modified or redistributed.**

---

## If you think something here is wrong

Licence compliance is not a formality and getting it wrong is not harmless. If
you believe a component is misattributed, missing a required notice, or that
the corresponding source is incomplete, please open an issue and it will be
corrected.
