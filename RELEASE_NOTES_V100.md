# PCM/DSD VU v1.0.0 — Release Notes

Initial official x86 / x64 release of **PCM/DSD VU**, a foobar2000 VU meter that automatically identifies PCM/DSD based on DoP signal analysis and supports both signal formats.

Includes standalone and Columns UI visualization contexts, 24 configurable external skins with 48 PCM/DSD-specific background images, Bar/Analog/Digital modes, and extensive needle/level/appearance options. See the [English user manual](https://github.com/jjh212/PCM_DSD_VU_RELEASE/blob/main/docs/USER_MANUAL_V100_EN.md) or [한국어 설명서](https://github.com/jjh212/PCM_DSD_VU_RELEASE/blob/main/docs/USER_MANUAL_V100_KO.md).

Install the `.fb2k-component` matching your player: `foo_pcm_dsd_vu_v1.0.0_x86.fb2k-component` for foobar2000 x86, or `foo_pcm_dsd_vu_v1.0.0_x64.fb2k-component` for foobar2000 x64, using Preferences → Components → Install. Restart, then verify `PCM/DSD VU / 1.0.0`. Actual x86 installation and PCM/DoP/DSD playback were verified by the project owner.

Release DLL SHA256 (x64): `0088C468F54E2994FBC09DF4A811F89445C0F0CDA4FB46661CE9D148E33055CC`.  Release DLL SHA256 (x86): `1C8E5C9D9CEAB8BA84AD162FB200A14E3DFC5C0FDC35549395813226C1AB109D`.

Build verification: VS 2026, MSVC v145, both x86 and x64 Release. No Windows FileVersion resource is claimed. Attach four build artifacts (two `.fb2k-component` files and two onedir `.zip` files) plus SHA256SUMS to the official release.

Binary assets should be attached to the Release only after SHA256/99-file archive validation on the Windows build host.
