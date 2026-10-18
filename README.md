<div align="center">

<img src="icon.jpg" alt="papascluckeria_nx" width="160">

# papascluckeria_nx

**Papa's Cluckeria To Go! on Nintendo Switch**

An unofficial Nintendo Switch port of the Android version of  
**Papa's Cluckeria To Go! — 1.0.4**

**By xFlippy**

[![Switch](https://img.shields.io/badge/Nintendo_Switch-Homebrew-E60012?style=for-the-badge&logo=nintendoswitch&logoColor=white)](#)
[![Ko-fi](https://img.shields.io/badge/Support_on_Ko--fi-FF5E5B?style=for-the-badge&logo=ko-fi&logoColor=white)](https://ko-fi.com/flippyy)

</div>

---

## About

`papascluckeria_nx` is an experimental standalone Nintendo Switch port targeting
Papa's Cluckeria To Go! Android 1.0.4 (ARM64).

It provides the compatibility layer that loads the Android package under Horizon
OS. It opens the game directly and needs no APK64 installation.

> Supply your own legally obtained APK. Game packages and native libraries are excluded from public downloads.

---

## Controls

Use the game's on-screen controls through the touchscreen, or enable the cursor:

- **Minus** toggles the outlined ice-blue cursor.
- **Left stick / D-pad** move it; **A** taps. Hold **A** while moving to drag.
- Touchscreen input takes priority. Release **A** before resuming cursor clicks.
- **Plus** exits to hbmenu.

### Launcher Dialog

The supplied Cluckeria 1.0.4 APK opens its original AIR activity directly.
Other dialogs keep their normal controls.

- Touch an action, or use **D-pad up/down** to choose and **A** to select.
- **L/R** scroll long dialogs; dragging also scrolls.
- **B** sends Back; dialogs may disable cancellation.
- **Plus** exits to hbmenu.

---

## Build

### Requirements

- [devkitPro](https://devkitpro.org/), devkitA64 and libnx
- Switch portlibs: Mesa/libdrm_nouveau, libvorbis/libogg, FreeType, curl,
  Mbed TLS and zlib
- Linux or WSL, GNU Make, Bash, Python 3.11+, curl, tar and patch
- A host C compiler, zlib and OpenSSL development headers for `make check`
- Host Mesa EGL/OpenGL libraries (libEGL.so.1 and libGL.so.1) for the real GLES cursor checks
- Your own legally obtained Papa's Cluckeria To Go! Android 1.0.4 ARM64 APK

### Compile

Open the source checkout:

```bash
cd papascluckeria_nx
```

Configure your devkitPro environment:

```bash
export DEVKITPRO=/opt/devkitpro
export DEVKITA64=$DEVKITPRO/devkitA64
export PATH=$DEVKITA64/bin:$DEVKITPRO/tools/bin:$PATH
```

Build the homebrew:

```bash
make -j$(nproc)
```

To rebuild from scratch:

```bash
make clean
make -j$(nproc)
```

The output is `papascluckeria_nx.nro`. 

## Running

Extract the SD ZIP onto your SD card and put your original APK beside the NRO:

```text
sd:/switch/papascluckeria_nx/
├── papascluckeria_nx.nro
└── game.apk
```

Use application/title takeover mode. Hold **R** while opening an installed game
to enter hbmenu, then launch Papa's Cluckeria To Go! Applet mode is not the
supported launch mode.

Only these two files need to be installed manually. On first launch or update,
the NRO unpacks its complete runtime to `cache/runtime.nro`, verifies its SHA-256,
then starts it through hbloader. This derived cache is about 56 MB and is rebuilt
if damaged or outdated. Allow about 120 MB free for cache updates. A normal
hbmenu/hbloader environment with next-load support is required.

The port creates `saves/`, `cache/`, `config/` and `logs/` as needed. Writable game
data stays under `sd:/switch/papascluckeria_nx/`. Keep `saves/` when updating;
replace only `papascluckeria_nx.nro`, leaving your APK and save folders in place.
The original Android package identity is preserved. This port does not import
saves from an existing APK64 installation automatically.

Run `make check` after building for bootstrap, storage and platform-data checks, and `make package` to
create source and SD ZIPs. Neither ZIP contains your game APK.

---

## Support

Bug reports with your game version, launch mode and relevant log output help
improve the port.

---

## Disclaimer

This is an unofficial fan project. It is not affiliated with or endorsed by
Flipline Studios.

Papa's Cluckeria To Go!, its trademarks, launcher artwork, audio and game assets
belong to their respective rightsholders. The homebrew menu author field
identifies the port maintainer, xFlippy. See `LICENSES.md` for inherited source
and third-party distribution requirements.

## Contribution

Bug reports, performance improvements and documented pull requests are welcome.
Include your game version, launch mode, reproduction steps and relevant log
output. Do not attach game packages, native libraries, personal save data or
credentials to public issues.
