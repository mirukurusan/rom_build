# LG SDM845 crDroid Builds

Unofficial [crDroid](https://crdroid.net/) builds for LG SDM845 devices.

The builds are source-level ports that add hardware features the generic
LineageOS trees do not provide — most notably VoLTE, the LG stock camera, 
and Hi-Fi Quad DAC high-resolution audio.

> These are unofficial builds. They are not affiliated with LG or the 
> crDroid project. Flash at your own risk.

## Supported devices

| Device | Codename |
| --- | --- |
| LG G7 ThinQ | `judyln` |
| LG V35 ThinQ | `judyp` |
| LG V40 ThinQ | `judypn` |

All three share the SDM845 platform and the common `sdm845-common` device trees.

## Highlights

- **VoLTE** — LG's IMS stack extracted from LG Velvet 4G (LM-G910EMW,
  Android 12) firmware and integrated at build time: platform-signed IMS
  applications, SELinux policy, framework patches, and MMTel SMS support.
  No root or runtime workarounds are required.
- **LG stock camera** (LG G7 ThinQ) — Full LG Camera stack: `LGCameraApp`,
  `LGCameraSolution`, AI SmartCam scene models, Cine/Film LUTs, ArcSoft and
  Morpho algorithm libraries, logical dual-camera support, and 4K60 recording.
- **Hi-Fi Quad DAC** (ES9218P) — Bit-perfect DIRECT output for Hi-Res PCM,
  the 44.1 kHz family no longer forced to 48 kHz, all 8 hardware digital
  filters exposed, persistent Sound Preset and L/R balance settings, and a
  Material 3 Quad DAC panel. 352.8 kHz material is decimated 2:1 to
  176.4 kHz to stay within SDM845 LPASS clock limits.
- **Dolby Atmos** support.
- **KernelSU-Next** kernels, packaged as AnyKernel3 flashable zips.
- **OTA updates** for all three devices through crDroid's Updater.
- **Platform fixes** — FM radio, in-call earpiece routing, speaker
  distortion/clipping, manual network scan, and per-device display cutout
  and rounded-corner handling.

## Downloads

- [GitHub Releases](https://github.com/mirukurusan/rom_build/releases)

## Repository layout

| Path | Purpose |
| --- | --- |
| `rom_build.sh` | Full pipeline: builds the ROM for all three devices, then KernelSU-Next boot images |
| `lg-sdm845.xml` | Local manifest overlay for the crDroid 16.0 source tree |
| `judyln.json`, `judyp.json`, `judypn.json` | crDroid OTA/update metadata, refreshed by the build scripts |
| `judyln.txt`, `judyp.txt`, `judypn.txt` | Release changelogs, shared by all three devices |
| `docs/` | Technical documentation (Chinese) for the major porting efforts |

## Documentation

The documents under `docs/` are written in Chinese and organized by topic and
language (`docs/<topic>/zh/`).

### Common device fixes

| Document | Topic |
| --- | --- |
| [01_AUDIO_EARPIECE_FIX.md](docs/common/zh/01_AUDIO_EARPIECE_FIX.md) | In-call earpiece routing (judyln) |
| [02_FM_RADIO_FIX.md](docs/common/zh/02_FM_RADIO_FIX.md) | FM radio: no audio, white noise, headset/speaker switching |
| [03_QUAD_DAC_SOUND_PRESET_FIX.md](docs/common/zh/03_QUAD_DAC_SOUND_PRESET_FIX.md) | Quad DAC Sound Preset mechanism and fix |
| [04_QUAD_DAC_VOLUME_BALANCE_FIX.md](docs/common/zh/04_QUAD_DAC_VOLUME_BALANCE_FIX.md) | Quad DAC L/R balance reset on pause/resume |
| [05_AUDIO_HIRES_44_1KHZ_FIX.md](docs/common/zh/05_AUDIO_HIRES_44_1KHZ_FIX.md) | Hi-Res direct passthrough across all sample rates |
| [06_AUDIO_HIRES_352_8KHZ_RESAMPLING_ANALYSIS.md](docs/common/zh/06_AUDIO_HIRES_352_8KHZ_RESAMPLING_ANALYSIS.md) | 352.8 kHz resampling and hardware clock limits |
| [07_DAC_PANEL_ISSUES.md](docs/common/zh/07_DAC_PANEL_ISSUES.md) | Quad DAC panel issues and redesign |
| [08_AUDIO_HIRES_DIRECT_FIX.md](docs/common/zh/08_AUDIO_HIRES_DIRECT_FIX.md) | Hi-Res DIRECT mode activation |
| [09_MANUAL_NETWORK_SCAN_FIX.md](docs/common/zh/09_MANUAL_NETWORK_SCAN_FIX.md) | Manual network scan failure |
| [10_VOLTE_SMS_INTEGRATION_AND_CARRIER_FIX.md](docs/common/zh/10_VOLTE_SMS_INTEGRATION_AND_CARRIER_FIX.md) | VoLTE SMS and multi-carrier compatibility |

### VoLTE

| Document | Topic |
| --- | --- |
| [BACKGROUND.md](docs/VoLTE/zh/BACKGROUND.md) | Architecture, firmware donor selection, and technical blockers |
| [IMPLEMENTATION_PLAN.md](docs/VoLTE/zh/IMPLEMENTATION_PLAN.md) | Step-by-step integration plan |
| [INTEGRATION_AND_TROUBLESHOOTING.md](docs/VoLTE/zh/INTEGRATION_AND_TROUBLESHOOTING.md) | Implemented changes and troubleshooting |
| [UNKNOWN_CARRIER_VOLTE_CSFB_ANALYSIS.md](docs/VoLTE/zh/UNKNOWN_CARRIER_VOLTE_CSFB_ANALYSIS.md) | VoLTE registration failure and 2G CSFB fallback analysis |

### LG Camera

| Document | Topic |
| --- | --- |
| [LG_CAMERA_INTEGRATION_SUMMARY.md](docs/LGCamera/zh/LG_CAMERA_INTEGRATION_SUMMARY.md) | Integration architecture, change list, and issue log |
| [LG_CAMERA_INTEGRATION_PLAN.md](docs/LGCamera/zh/LG_CAMERA_INTEGRATION_PLAN.md) | Integration plan and implementation steps |

## Support the project

Porting modern Android (Android 16) to legacy SDM845 platforms and resolving
long-standing proprietary hardware issues (VoLTE, Quad DAC, stock camera) takes
a significant amount of time, patience, iterative debugging, and hardware testing.

These builds will always be free and open-source. However, if this project has helped
revive your LG device as a daily driver or dedicated music player, and you'd like
to support ongoing maintenance, server build costs, or just buy me a coffee, donations
are greatly appreciated!

- **Afdian:** [afdian.com/a/mirukurusan](https://afdian.com/a/mirukurusan)

*(Donations are completely voluntary and do not include exclusive perks, builds, or direct technical support.)*

## Credits

- [crDroid](https://crdroid.net/) and [LineageOS](https://lineageos.org/) for
  the base ROM and device tree infrastructure
- [TheMuppets](https://github.com/TheMuppets) for proprietary vendor blobs
- [KernelSU-Next](https://github.com/KernelSU-Next/KernelSU-Next)
- LG Velvet 4G (LM-G910EMW) firmware as the IMS donor