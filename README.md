# Crimson Desert on a Radeon RX 580 — Linux / Proton port

**Crimson Desert refuses to start on AMD Polaris cards.** This makes it run —
on Linux, under Proton, without touching your Proton installation.

[![Download](https://img.shields.io/badge/download-v1.0.0%20%C2%B7%206.4%20MB-2B5A87?style=flat-square)](https://github.com/njtechyt/RX580-Crimson-Desert-Fix-Linux-only/releases/latest/download/RX580-Crimson-Desert-DLLs.zip)
![OS](https://img.shields.io/badge/OS-Linux%20%2F%20Proton-informational?style=flat-square)
![GPU](https://img.shields.io/badge/GPU-Polaris%20%2F%20GCN4-informational?style=flat-square)
[![Game](https://img.shields.io/badge/game-Crimson_Desert_PC-informational?style=flat-square)](https://store.steampowered.com/search/?term=Crimson+Desert)
![Licence](https://img.shields.io/badge/licence-Apache--2.0%20%2B%20LGPL--2.1-lightgrey?style=flat-square)

The game asks for Direct3D 12 **feature level 12_1** and **native 16-bit float**
shaders. An RX 580 has neither. It's not that the game runs badly on Polaris —
it checks, doesn't like the answer, and stops.

This package drops two patched vkd3d-proton DLLs next to the game and tells
Proton to prefer them. The DLLs answer those capability questions the Polaris
way and repair every place where that answer needs help — forged feature
reporting, per-stage FP16 handling, a workaround for a Polaris shader-compiler
fault, and an emulation of GPU-driven command submission that also fixes the
frame-rate collapse it used to cause. The game now reaches gameplay and
renders correctly.

This is a Linux/Proton port of the Windows fix by
[Vidith007](https://github.com/Vidith007/RX-580-CRIMSON-DESERT-FIX) — same
remedy, different delivery: no shim, no `.ini`, no Proton files modified.

---

## Read this before you install

> [!WARNING]
> **If you have an RX 5000 series or newer, do not install this.** RDNA and
> later report feature level 12_1 natively. This fix exists only to paper over
> gaps that Polaris has and newer cards don't — on those cards it can only
> make things worse.

> [!CAUTION]
> Tested on an RX 580 under Proton over about a week of gameplay. It is
> unofficial, unaffiliated with AMD, Valve or Pearl Abyss, and warranted for
> nothing. Reverting is deleting two files — see Install.

---

## Requirements

| | |
|---|---|
| **GPU** | AMD Polaris / GCN4 — RX 470, 480, 570, 580, 590 |
| **Driver** | A Vulkan-capable driver for your card (Mesa RADV recommended) |
| **OS** | Linux 64-bit |
| **Proton** | Any recent Proton / GE-Proton |
| **Game** | Crimson Desert, PC |

---

## Install

Full guide with troubleshooting: [`INSTALL.md`](INSTALL.md). Short version:

1. Download **`RX580-Crimson-Desert-DLLs.zip`** from the
   [releases page](https://github.com/njtechyt/RX580-Crimson-Desert-Fix-Linux-only/releases)
   and unzip it.
2. Copy `d3d12.dll` and `d3d12core.dll` from `x86_64/` into the folder with
   the game's `.exe` — same folder, alongside it, nothing else.
3. Launch the game normally — no launch options needed. First launch
   compiles shaders and is slow; later launches reuse the cache.

4. To revert: delete the two DLLs. Nothing else on your system was touched.

---

## Verify your download

From the folder you unzipped into:

```bash
sha256sum x86_64/d3d12.dll x86_64/d3d12core.dll
```

Compare against [`SHA256SUMS.txt`](SHA256SUMS.txt).

---

## What's in this repo

```
fix/                      the two DLLs that go next to the game .exe
fix/licenses/             upstream licence texts, unedited
source/                   the modified vkd3d-proton source, as a patch
RX580-Crimson-Desert-DLLs.zip   everything above, packaged
README.md / INSTALL.md / CHANGELOG.md   docs
LICENSE / NOTICE / THIRD-PARTY-NOTICES.md / SHA256SUMS.txt   legal + checksums
```

---

## Credit

The hard parts were written by other people:

- **Vidith007**, for the
  [RX-580-CRIMSON-DESERT-FIX](https://github.com/Vidith007/RX-580-CRIMSON-DESERT-FIX)
  this port is based on — the fix itself is his work.
- **Hans-Kristian Arntzen**, for
  [vkd3d-proton](https://github.com/HansKristian-Work/vkd3d-proton).
- **Józef Kucia** (1985–2020), who wrote vkd3d, which none of this exists without.
- **All vkd3d-proton contributors** — the unedited `AUTHORS` file ships in
  [`fix/licenses/`](fix/licenses/).
- **Valve Corporation**, which funds the work that makes D3D12 games run on Vulkan at all.
- **Pearl Abyss** made Crimson Desert. No file of theirs is modified or redistributed here.
- AI assistance was used to speed up this work.

## Licences

Three licences, and it matters which is which — see
**[THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md)** and **[NOTICE](NOTICE)**.

- **Original work here** (this port, packaging, docs) — Apache-2.0, see [`LICENSE`](LICENSE).
- **`fix/d3d12core.dll` and `fix/d3d12.dll`** — vkd3d-proton, **LGPL-2.1-or-later**,
  modified builds. Corresponding source:
  [`source/RX580-proton-build.patch`](source/RX580-proton-build.patch).
- **dxil-spirv**, vendored inside that build — MIT.

Apache-2.0 does **not** and cannot cover the vkd3d-proton binaries. They stay LGPL.
