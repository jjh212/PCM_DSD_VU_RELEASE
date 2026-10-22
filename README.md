# PCM/DSD VU v1.0.0

**PCM/DSD VU** is a foobar2000 Windows x86/x64 visualization component offering VU meters for **PCM and DSD** playback.

## Core features / 주요 기능

- **Automatic PCM/DSD identification by interpreting actual DoP signals.** DoP transports DSD data in PCM-formatted frames; it is not an audio conversion to PCM.
- **Full PCM and DSD meter operation**, as confirmed by the project owner.
- Independent left/right meters and horizontal, vertical, single-channel layout choices.
- Bar Meter, Analog, and Digital displays; RMS / Peak / Crest Factor plus LUFS-M/S/I and preliminary LRA indications.
- Selectable needle movement, decay, tuning controls, and color themes.
- External skin system: **24 `.vusk` profiles**, **48 PCM/DSD background PNGs**, **24 needle PNGs**, **2 auxiliary PNGs** across 4 design families, 2 frame options, and 3 geometries.
- Standalone window and Columns UI display contexts, as captured in the supplied foobar2000 screenshots.

## Documentation / 설명서

- [한국어 사용자 설명서](docs/USER_MANUAL_V100_KO.md)
- [English user manual](docs/USER_MANUAL_V100_EN.md)
- [v1.0.0 change log / 변경내역](CHANGELOG.md)
- [Screenshot inventory with SHA256](docs/SCREENSHOT_MANIFEST_V100.tsv)

The manuals include **30 actual screenshots**, including the foobar2000 Components listing showing **PCM/DSD VU 1.0.0** and nine examples of Bar/Analog/Digital metering. No promotional mockups are presented as runtime captures.

## Installation / 설치

Select the package matching your foobar2000 architecture:

- **x86 / 32-bit:** `foo_pcm_dsd_vu_v1.0.0_x86.fb2k-component`.
- **x64 / 64-bit:** `foo_pcm_dsd_vu_v1.0.0_x64.fb2k-component`.

Open `Preferences → Components → Install` in foobar2000, select the matching package, restart the player, then verify **PCM/DSD VU 1.0.0**. Open the meter through `View → Visualizations → PCM/DSD VU`.

**Build and real-host verification (2026-10-23):** Windows x86 and x64 Release; MSVC v145 (VS 2026); each build: zero errors and ten warnings. The user verified both PCM and DoP/DSD meter operation on the x86 test host, and the x64 installation is confirmed.

| Architecture | Component DLL SHA256 | Verification |
|---|---|---|
| x86 (PE32, `0x014C`) | `1C8E5C9D9CEAB8BA84AD162FB200A14E3DFC5C0FDC35549395813226C1AB109D` | Build, 99-file package, foobar2000 2.25.8 x86 installation and playback verified |
| x64 (PE32+, AMD64) | `0088C468F54E2994FBC09DF4A811F89445C0F0CDA4FB46661CE9D148E33055CC` | Build, 99-file package and foobar2000 installation verified |

Windows `FileVersion`/`ProductVersion` resource fields were not populated in the inspected x64 build; foobar2000 Components explicitly displays the software version **1.0.0**. The distribution uses ordinary multi-file component archives, never a single-executable bundle.

The exact quantitative metering algorithms, supported Native DSD routes, rate ceilings, and any standards certification are not claimed without separate source-level or measurement evidence.
