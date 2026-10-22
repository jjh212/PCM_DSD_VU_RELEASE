# PCM/DSD VU v1.0.0

**PCM/DSD VU** is a foobar2000 Windows x64 visualization component offering VU meters for **PCM and DSD** playback.

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

The manuals include **28 actual screenshots**, including the foobar2000 Components listing showing **PCM/DSD VU 1.0.0** and nine examples of Bar/Analog/Digital metering. No promotional mockups are presented as runtime captures.

## Installation / 설치

Use the **x64** component `foo_pcm_dsd_vu_v1.0.0_x64.fb2k-component`. Open foobar2000 `Preferences → Components → Install`, select the package, restart, and verify `PCM/DSD VU` version **1.0.0**. Open the meter via `View → Visualizations → PCM/DSD VU`.

**Build-proven:** VS 2026, MSVC v145, Windows x64 Release. Component DLL `foo_pcm_dsd_vu.dll` — 226,304 bytes; SHA256 `0088C468F54E2994FBC09DF4A811F89445C0F0CDA4FB46661CE9D148E33055CC`.

**Compatibility scope:** x64 was built and exercised in the user's foobar2000 setup; no x86 distribution is claimed. Windows `FileVersion`/`ProductVersion` metadata fields were empty in the inspected build; foobar2000's component registration explicitly displays **1.0.0**.

The exact quantitative metering algorithms, supported Native DSD routes, rate ceilings, and any standards certification are not claimed without separate source-level or measurement evidence.