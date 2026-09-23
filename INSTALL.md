# Install — Crimson Desert RX 580 fix (Linux / Proton)

## 1. Download and unzip

Get **`RX580-Crimson-Desert-DLLs.zip`** from the
[releases page](https://github.com/njtechyt/RX580-Crimson-Desert-Fix-Linux-only/releases)
and unzip it. You need two files from `x86_64/`:

```
x86_64/d3d12.dll
x86_64/d3d12core.dll
```

Verify before use (see "Verify" below).

## 2. Put the DLLs next to the game

Find the folder containing the game's `.exe` (in your Steam library:
`steamapps/common/...`, exact folder varies). Copy both DLLs there, alongside
the `.exe`. Nothing else goes anywhere — no Proton files are modified, no
system files, no registry.

Your folder should look like:

```
<game dir>/
    <Game>.exe                (already there, untouched)
    d3d12.dll                 <- from x86_64/
    d3d12core.dll             <- from x86_64/
```

## 3. Launch

Just launch the game normally — no launch options needed. Proton picks up the
two DLLs from the game folder on its own.

First launch compiles every shader from scratch — expect a long wait, then
much faster launches afterwards.

## 5. Revert (if needed)

Delete the two DLLs, clear the launch options. You are exactly where you
started.

## Verify

```bash
cd <unzipped folder>
sha256sum x86_64/d3d12.dll x86_64/d3d12core.dll
```

Expected (v1.0.0):

```
b569eee55b71c95f5fd79641ae123264c63d64885b555b46ba15d4aba7b5aff4  x86_64/d3d12.dll
fd0225e6727da1df5f1324f3b47ffd802681dd0d938a680063feda70cf02a5f4  x86_64/d3d12core.dll
```

Full list (both architectures + patch): [`SHA256SUMS.txt`](../SHA256SUMS.txt).

## Troubleshooting

| Symptom | Fix |
|---|---|
| **Game behaves exactly as before, fix seems ignored** | Confirm both DLLs sit *next to the `.exe`*, not in a subfolder. If they do and it's still ignored, your Proton loads builtins first — force yours with `WINEDLLOVERRIDES="d3d12=n,b;d3d12core=n,b" %command%` in Launch Options. |
| **Game exits immediately / D3D12 errors** | Confirm both DLLs sit *next to the `.exe`*, not in a subfolder. Check the Proton version didn't change under you. |
| **Low frame rate** | Expected: the multi-draw batching is dormant in this build (see above), so the frame rate is whatever the correctness fixes deliver. |
| **Need real diagnostics** | Logging is fully working in this build: add `VKD3D_DEBUG=err` to the launch options and read the Proton log. |
| **Nothing helped** | Delete the DLLs, clear launch options — clean revert, then open an issue with your exact GPU, driver (Mesa version), Proton version, and RAM. |
