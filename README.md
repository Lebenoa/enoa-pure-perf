# Enoa's Pure Perf

A client-side Fabric modpack for Minecraft 26.2 focused on rendering and performance. ***Despite the name, Nvidium is the only NVIDIA-specific mod.***

> [!NOTE]
> `master` stays on Minecraft 26.2 to retain Nvidium and the other mods removed for compatibility with 26.3. For the newer pack, see the [26.3 branch](https://github.com/Lebenoa/enoa-pure-perf/tree/26.3) and its README.

Prebuilt 26.2 packs are available for [Prism Launcher](https://github.com/Lebenoa/enoa-pure-perf/releases/tag/26.2.1) and [NoRisk Client](https://github.com/Lebenoa/enoa-pure-perf/releases/tag/26.2.1). The newer v0.3.0 release targets 26.3.

## Features

- Render with Sodium and Iris Shaders; use Nvidium's alternative renderer on supported NVIDIA GPUs when shaders are inactive.
- Use client-side performance mods that stay out of gameplay's way.
- Export the recorded mod versions to a `.mrpack` or a `.noriskpack` for import into a compatible launcher.

## `.mrpack` distribution

InstaPack has third-party distribution disabled on CurseForge, so I'm not comfortable shipping a prebuilt `.mrpack` that bundles its jar. That's my choice, not a license — the mods still belong to their authors. The installer scripts build the standard `.mrpack` on your machine instead.

My [packwiz fork](https://github.com/Lebenoa/packwiz/releases) supports `packwiz modrinth export --no-bundle`, which the prebuilt `.mrpack` uses to reference InstaPack by its CurseForge download URL instead of bundling its jar. Modrinth rejects CurseForge CDN URLs, launcher support varies, and launchers may show a provenance warning.

## Installation

### NoRisk Client (verified)

Download `enoa-pure-perf.noriskpack` from the [26.2.1 release](https://github.com/Lebenoa/enoa-pure-perf/releases/tag/26.2.1) and import it into NoRisk Client.

To build a NoRisk pack yourself, download and extract the [master ZIP](https://github.com/Lebenoa/enoa-pure-perf/archive/refs/heads/master.zip), then run this from the extracted folder with a [packwiz fork](https://github.com/Lebenoa/packwiz/releases) that supports `norisk export` on PATH:

```bash
packwiz norisk export -o enoa-pure-perf.noriskpack
```

Import the resulting file into NoRisk Client. The export sets the profile icon configured in `pack.toml`; fork release **v0.0.2+** supports this command, but upstream packwiz does not.

### Prism Launcher (verified) and other `.mrpack` launchers

Download `enoa-pure-perf.mrpack` from the [26.2.1 release](https://github.com/Lebenoa/enoa-pure-perf/releases/tag/26.2.1) and import it into Prism Launcher or another launcher that accepts CurseForge download URLs. The v0.3.0 `.mrpack` is for 26.3.

To build the standard `.mrpack` locally instead, download the repository using **Code → Download ZIP**, or [download the master ZIP directly](https://github.com/Lebenoa/enoa-pure-perf/archive/refs/heads/master.zip). Extract it before running either installer; Git is not required.

- Targets Minecraft **26.2** and Fabric **0.20.1** (packwiz format **1.1.0**); Java **25 or later**, as required by the selected mods.
- **Windows:** PowerShell 5.1 or later — its downloader and ZIP extraction commands are built in.
- **Linux / macOS:** bash and curl, plus tar when the script must fetch the pack.
- Internet access, and a launcher that imports `.mrpack` files.

**Windows:** double-click `install.cmd` in the extracted folder. It runs `install.ps1` and keeps the window open so you can read the result or any errors. No administrator privileges are required. Alternatively, open PowerShell in the extracted folder and run:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File .\install.ps1
```

**Linux / macOS:** open a terminal in the extracted folder and run:

```bash
bash install.sh
```

The scripts reuse `packwiz` on PATH, or download fork release **v0.0.2** if none is found (Windows selects the amd64 build; Unix selects by OS and architecture), then export `enoa-pure-perf.mrpack`. They do not install a launcher or Minecraft.

> [!TIP]
> **Recommended: use the [fork release](https://github.com/Lebenoa/packwiz/releases) (v0.0.2 or later).** It can fetch InstaPack automatically and supports `packwiz norisk export` for NoRisk Client. If `packwiz` is already on PATH, the scripts reuse it without verifying that it is the fork; an upstream binary may require a manual download. See [Acknowledgments](#acknowledgments) for the API-key explanation.

**With upstream packwiz:** if export requests a manual download, obtain [InstaPack 1.0.0 for Fabric 26.2](https://www.curseforge.com/minecraft/mc-mods/instapack/files/9099255) and follow packwiz's prompt before retrying. Do not assume a failed export produced a complete pack.

> [!NOTE]
> After changing the pack metadata, run the installer again to generate a new `.mrpack`.

After export succeeds, import `enoa-pure-perf.mrpack` into a compatible launcher, such as Prism Launcher or ATLauncher. Launch the imported Minecraft **26.2** / Fabric **0.20.1** instance.


## Defaults

| Setting | Default |
|---|---|
| Sneak / Sprint | **Left Ctrl** / **Left Shift** (swapped from vanilla) |
| FOV | 103° |
| FOV effects | ~2.29% |
| GUI scale | 2 |
| VSync / FPS limit | Off / 200 |
| Render / simulation distance | 8 / 8 chunks |
| Mipmap level / clouds | 2 / fast |
| Screen effects | Off |
| Mouse sensitivity / damage tilt | 25% / 50% |
| Auto-jump / pause on lost focus | Off |
| Advanced item tooltips | On |
| Master volume | ~14.57% |
| Music / ambient volume | Muted |
| Swap offhand key | Vanilla default |
| Iris max shadow render distance | 6 |

The pack also ships configs for Dynamic FPS, More Culling, and Mod Menu.

Importing `options.txt` or these configs into an existing instance replaces that instance's saved settings; these defaults are intended for a fresh instance.

## Why?

Honestly? [Fabulously Optimized](https://modrinth.com/modpack/fabulously-optimized) ships mods I never use and is missing ones I always want. So this is my own take — most of the mods I actually play with, minus the stuff I'd just turn off anyway.

## Mods

All 23 mods, grouped by purpose. The Side column reproduces this pack's metadata (`client` or `both`); it is not a guarantee of server compatibility.

| Mod | Side | What it does |
|---|---|---|
| **Performance** | | |
| [Sodium](https://modrinth.com/mod/AANobbMI) | client | Replaces Minecraft's renderer with an optimized one for smoother gameplay. |
| [Lithium](https://modrinth.com/mod/gvQqBUqZ) | both | Optimizes game logic (physics, mob AI, block ticks) without changing vanilla behavior. |
| [FerriteCore](https://modrinth.com/mod/uXXizFIs) | both | Reduces Minecraft's memory usage. |
| [BadOptimizations](https://modrinth.com/mod/g96Z4WVZ) | client | Applies targeted micro-optimizations to frequently-run client code. |
| [ModernFix-mVUS](https://modrinth.com/mod/TjSm1wrD) | both | Extends ModernFix to additional Minecraft versions, retaining performance, memory, and bug fixes. |
| [ImmediatelyFast](https://modrinth.com/mod/5ZwdcRci) | client | Optimizes the immediate-mode rendering path (HUD, GUIs, text). |
| [Entity Culling](https://modrinth.com/mod/NNAgCjsB) | client | Skips rendering hidden entities and block entities. |
| [More Culling](https://modrinth.com/mod/51shyZVL) | client | Skips rendering hidden block faces and other culling improvements. |
| [Better Block Entities](https://modrinth.com/mod/ONZm0H7Y) | client | Optimizes block entity rendering, including chests and signs, while preserving animations. |
| [Dynamic FPS](https://modrinth.com/mod/LQ3K71Q1) | client | Adjusts frame rate, volume, and resource use when backgrounded, idle, or on battery. |
| [FastQuit](https://modrinth.com/mod/x1hIzbuY) | client | Lets you leave a world while saving finishes in the background. |
| [Ixeris](https://modrinth.com/mod/p8RJPJIC) | client | Reduces input-polling overhead, especially with high-polling-rate mice on Windows. |
| [InstaPack](https://www.curseforge.com/minecraft/mc-mods/instapack) | both | Optimizes resource reloads, skips unchanged server packs, and caches packs to avoid repeat downloads. |
| **Rendering & visuals** | | |
| [Iris Shaders](https://modrinth.com/mod/YL57xq9U) | client | Loads OptiFine-style shader packs alongside Sodium. |
| [Nvidium](https://modrinth.com/mod/SfMw2IZN) | client | Replaces Sodium's terrain renderer on mesh-shader-capable NVIDIA GPUs (GTX 16-series and supported newer cards); disables itself while Iris shaders are active. |
| **Interface & QoL** | | |
| [Mod Menu](https://modrinth.com/mod/mOgUt4GM) | client | Browse installed mods and open their config screens from the title screen. |
| [Reese's Sodium Options](https://modrinth.com/mod/Bh37bMuy) | client | Reorganized, searchable Sodium video settings screen. |
| [Sodium Extra](https://modrinth.com/mod/PtjYWJkn) | client | Extra graphics toggles Sodium lacks (fog, animations, particles). |
| [ExploitPreventer](https://modrinth.com/mod/VdINCTcD) | client | Blocks known client-side exploits. |
| [Remove Reloading Screen](https://modrinth.com/mod/ZP7xHXtw) | client | Keeps the game accessible during resource reloads, retaining a progress bar. |
| **Libraries & dependencies** | | |
| [Fabric API](https://modrinth.com/mod/P7dR8mSH) | both | Core APIs most Fabric mods depend on. |
| [Cloth Config API](https://modrinth.com/mod/9s6osm5g) | both | Config screen library used by other mods. |
| [YetAnotherConfigLib (YACL)](https://modrinth.com/mod/1eAoo2KR) | client | Config screen library used by other mods. |

## Acknowledgments

This pack is maintained with a personal fork of the packwiz CLI: [Lebenoa/packwiz](https://github.com/Lebenoa/packwiz), forked from [packwiz/packwiz](https://github.com/packwiz/packwiz). As of v0.0.2, the fork also adds a `norisk` command for exporting NoRisk Client packs.

The fork ships the trusted [MultiMC/PolyMC/Prism CurseForge API key](https://github.com/enjarai/the-curseforge-api-key) and, since v0.0.2, the `norisk` export command. CurseForge only returns `downloadUrl` for projects with third-party distribution disabled (like InstaPack) when the request uses a key it trusts; with an untrusted key the file comes back without a URL and export fails. Upstream removed this key, so its exports degrade that mod to a manual download — the fork resolves and bundles it automatically ([release binaries](https://github.com/Lebenoa/packwiz/releases) for Windows/macOS/Linux).

## License

No license file or license declaration is present in this repository. All rights reserved unless the author grants permission; contact the author before redistributing.
