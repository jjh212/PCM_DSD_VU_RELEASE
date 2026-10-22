# PCM/DSD VU v1.0.0 — 공식 사용자 설명서

> **공식 사용자 설명서 · 2026-10-23 · Windows x86/x64 / foobar2000**  
> 실제 사용자 제공 스크린샷 30장과 x86/x64 Release 빌드 기록을 바탕으로 작성했습니다. foobar2000 Components에서 `PCM/DSD VU 1.0.0` 표시가 확인되었습니다.

## 1. 개요

**PCM/DSD VU**는 foobar2000에서 사용할 수 있는 VU Meter 시각화 컴포넌트입니다. 제공된 화면에서 독립 VU 창, 왼쪽/오른쪽 미터, 바늘과 스킨 배경, 우클릭 설정 메뉴를 확인했습니다. 독립 창의 외형을 아래에서 볼 수 있습니다.

![독립 PCM/DSD VU 창](images/v100/meter_standalone.png)

*그림 1. AUDIOENGINE 외형의 독립 창. 촬영 시 두 미터와 스킨 배경이 보입니다.*

컴포넌트는 2026-10-23 격리 환경에서 MSVC v145를 이용해 **x64 Release 컴파일과 링크에 성공**했습니다(컴파일 오류 0개, 경고 10개). 빌드된 DLL의 SHA256은 `0088C468F54E2994FBC09DF4A811F89445C0F0CDA4FB46661CE9D148E33055CC`입니다. 이 DLL의 빌드 검증과 foobar2000 Components의 버전 표시 확인은 각각 별도 증거입니다.

## 2. 핵심 기능 — PCM/DSD 자동 판별 및 완전 동작

### 2.1 DoP 신호 분석으로 PCM/DSD 자동 식별

**PCM/DSD VU는 실제 DoP(DSD over PCM) 신호를 해석하여 PCM과 DSD를 자동으로 판별합니다.** 파일 확장자나 재생목록 이름을 기준으로 수동 선택하는 방식이 아닙니다. 재생 신호가 PCM이면 PCM 미터로, DoP를 통해 DSD가 확인되면 DSD 미터로 동작하는 것이 제품의 핵심 기능입니다.

**DoP는 DSD를 PCM 음원으로 변환하는 기술이 아닙니다.** 전송을 위해 PCM 형식의 프레임에 DSD 데이터와 식별 마커를 배치하는 형식입니다. DoP 공개 규격은 대표적으로 `0x05`와 `0xFA` 식별 마커가 교대로 나타나는 구조를 정의합니다. 이 규격 설명은 DoP의 원리를 이해하기 위한 **외부 표준 참조**이며, 이 컴포넌트가 사용하는 내부 투표 횟수·전환 지연·지원 DSD 배수까지 인증하는 내용은 아닙니다.

- 형식 판별: 신호 기반 자동 처리, 수동 PCM/DSD 선택 불필요
- 정상 동작: **PCM과 DSD 양쪽에서 VU 미터의 레벨·바늘 표시 기능 지원** (프로젝트 소유자 확인 사항)
- 배경 리소스: PCM용과 DSD용을 별도 제공하여 형식별 스킨 표현 구성
- 확인 범위: DoP 기반 자동 판별. **Native DSD 직접 입력 경로 및 모든 DSD 배수의 포괄적 지원을 여기에서 주장하지 않음**

**DoP 규격 문서:** [DoP open Standard, Version 1.1 (2012)](https://dsd-guide.com/sites/default/files/white-papers/DoP_openStandard_1v1.pdf)

### 2.2 화면에 표시되는 레벨과 지표

VU 바늘의 표시 모드는 `RMS + Peak`, `RMS`, `Peak` 가운데 선택합니다. 보조 표시로 `Crest Factor`와 `LUFS / LRA`를 켜고 끌 수 있습니다. **Crest Factor**는 일반적으로 피크 레벨과 RMS 레벨 사이의 차이, **LUFS**는 체감 음량을 나타내는 단위, **LRA**는 음량 변화 폭을 표현하는 지표입니다. 이러한 용어 설명은 일반적인 오디오 계측 개념이며, 제품의 특정 계산식이나 EBU R128 인증을 의미하지 않습니다.

각 표시 옵션은 바늘의 관성·감쇠 제어(`Movement`, `Decay`, `Tuning`)와 구별됩니다. PCM/DSD 자동 판별, 레벨 표시 방식, 바늘 물리 애니메이션은 서로 다른 기능입니다.

**추가 참조:** [EBU R128 — Audio loudness normalisation](https://tech.ebu.ch/docs/r/r128v4_0.pdf)

## 3. 실행 방법

foobar2000에서 **View → Visualizations → PCM/DSD VU**를 선택합니다. 사용자가 제공한 DarkOne UI 화면에서 실행 메뉴 위치가 확인됩니다.

![foobar2000 실행 메뉴](images/v100/launch_menu.png)

*그림 2. View → Visualizations의 PCM/DSD VU 항목.*

독립 VU 창에서 마우스 오른쪽 버튼을 눌러 설정 메뉴를 엽니다. 아래 항목의 선택 표시는 **촬영 당시 상태**입니다. 초기값·재시작 후 유지 여부는 별도 실사용 검증 대상입니다.

## 4. 우클릭 메뉴

### 4.1 Layout — 표시 채널과 창 배치

![Layout 메뉴](images/v100/layout_menu.png)

| 화면 항목 | 의미/기능 범위 | 화면 상태 |
|---|---|---|
| `Left + Right (Vertical)` | L/R 세로 배치 선택 | 미선택 |
| `Left + Right (Horizontal)` | L/R 가로 배치 선택 | **선택됨** |
| `Left Only` | 왼쪽 채널만 표시하도록 선택 | 미선택 |
| `Right Only` | 오른쪽 채널만 표시하도록 선택 | 미선택 |
| `Lock Aspect Ratio` | 화면 비율 잠금 옵션 | **선택됨** |

*그림 3. Layout 하위 메뉴와 촬영 당시 선택 표시.*

### 4.2 Levels — 표시 레벨 모드

![Levels 메뉴](images/v100/levels_menu.png)

`RMS + Peak`(선택됨), `RMS`, `Peak` 세 가지를 선택할 수 있습니다. 이 화면은 모드 존재 여부를 보여주며, 측정 윈도 길이·피크 산출식·VU 보정값까지 입증하지는 않습니다.

### 4.3 Movement — 바늘 이동 방식

![Movement 메뉴](images/v100/movement_menu.png)

`No Inertia`(선택됨), `Curve Fit`, `Spring-Mass-Damper`를 선택할 수 있습니다. 각각의 동작 수식, 반응 특성 및 수치 조건은 현재 스크린샷에 포함되지 않습니다.

### 4.4 Decay — 감쇠 설정

![Decay 메뉴](images/v100/decay_menu.png)

| 메뉴 | 화면 표시 |
|---|---|
| `Fast (Direct)` | 선택 가능 |
| `Normal (350 ms)` | **선택됨** |
| `Slow (900 ms)` | 선택 가능 |
| `Custom (Tuning)` | 사용자 조정 항목 |

*단위 ms와 표기값은 실제 메뉴에 나온 그대로 기재했습니다.*

### 4.5 Display — 추가 지표 표시

![Display 메뉴](images/v100/display_menu.png)

`Show Crest Factor`와 `Show LUFS / LRA`가 제공되고 **둘 다 체크**돼 있습니다. 이 지표들이 실제 계측 화면에 표시되는 모습은 아래의 Bar/Analog/Digital 갤러리에서 확인할 수 있습니다. 계산식과 표준 적합성에 대한 인증은 별개입니다.

### 4.6 Appearance — 외형과 스킨

![Appearance → External Skins 메뉴](images/v100/appearance_external.png)

![Appearance → Color Theme 메뉴](images/v100/appearance_color.png)

`Bar Meter`, `Analog`, `Digital`, `Color Theme`, `External Skins` 항목이 확인됩니다. `Color Theme`에는 `Studio Dark`, `Warm Amber`, `Classic Ivory`가 표시됩니다. `External Skins` 목록은 제공된 이미지에서 오른쪽이 잘렸으므로 전체 테마 이름과 순서를 임의로 기재하지 않았습니다.

STEP25 최종 파일 목록을 실제로 집계한 결과 다음 구조가 확인됩니다.

| 분류 | 구분 | 수량 |
|---|---|---:|
| 디자인 | Default(은색 메탈), AudioEngine, ClassicStereo, StudioBlack | 4계열 |
| 테두리 | `None`, `Border` | 2종 |
| 형상 | `Circle`, `Square`, `Half` | 3종 |
| 스킨 프로파일 | 4 × 2 × 3 (`.vusk`) | **24개** |
| 형식별 배경 | PCM/DSD 각각 제공 (24 × 2) | **48개 PNG** |
| 바늘 | 프로파일별 PNG | 24개 |
| 기타 | Clear Full/Half 보조 이미지 | 2개 |

즉, **48개는 배경 이미지의 수**이며, 구성 파일은 24개 프로파일입니다. 메뉴에서 보이는 선택 항목의 수와 파일 수는 구별해야 합니다. `Circle`과 `Square`는 FULL 형상, `Half`는 HALF 형상 계열입니다. 최종 설계 이미지 규격은 FULL 1936×1292, HALF 1936×644를 사용합니다. 이는 스킨 리소스 기준이지 실행 창의 고정 크기가 아닙니다.

### 실제 스킨 화면 갤러리

| 디자인 | 프레임 없음 | 프레임 있음 |
|---|---|---|
| Default / 실버 메탈 | [기본 화면](images/v100/meter_standalone.png) | ![실버 메탈 프레임](images/v100/theme_default_border.png) |
| AudioEngine / 앰버 | ![앰버](images/v100/theme_audioengine_none.png) | ![앰버 프레임](images/v100/theme_audioengine_border.png) |
| Classic Stereo | ![클래식](images/v100/theme_classic_none.png) | ![클래식 프레임](images/v100/theme_classic_border.png) |
| Studio Black | ![스튜디오 블랙](images/v100/theme_studioblack_none.png) | ![스튜디오 블랙 프레임](images/v100/theme_studioblack_border.png) |

*그림 11~17. 사용자 제공 실사용 스크린샷. 모두 한 형태의 독립 창을 촬영한 예이며 Circle/Square/Half 전체 형상 변형을 대표하지 않습니다.*

### 4.7 Tuning — 이동 파라미터

![Tuning 대화상자](images/v100/tuning_dialog.png)

| 필드 | 촬영 당시 표시값 | 단위 |
|---|---:|---|
| `Rise` | 80 | ms |
| `Decay Custom` | 200 | ms |
| `Peak Hold` | 0 | ms |
| `Spring Speed` | 7 | Hz |
| `Spring Damping` | 70 | % |

`OK`, `Cancel` 버튼이 있습니다. **이 표의 값은 기본값이나 권장값이 아니라 캡처 시점에 표시된 값**입니다. 허용 입력 범위는 이 화면만으로 확인할 수 없습니다.

### 4.8 Options — 표시·진단·초기화

![Options 메뉴](images/v100/options_menu.png)

| 메뉴 항목 | 촬영 당시 표시 |
|---|---|
| `Design Mode` | **체크됨** |
| `Show PCM/DSD Format` | 체크 없음 |
| `Show FPS` | 체크 없음 |
| `Show Console Logs` | 체크 없음 |
| `Always on Top` | 체크 없음 |
| `Reset Options to Defaults` | 실행 항목 |

`Reset Options to Defaults`의 초기화 범위와 확인 대화상자 유무는 현재 캡처에서 확인되지 않습니다.

## 5. Bar Meter / Analog / Digital — 실제 계측 화면

`Appearance`에서 선택 가능한 Bar Meter, Analog, Digital의 실제 화면입니다. 아래는 **세 가지 테마 × 세 가지 표시 방식**의 사용자 캡처 9장입니다.

| Theme / 테마 | Bar Meter | Analog | Digital |
|---|---|---|---|
| Studio Dark | ![Studio Dark Bar](images/v100/studio_dark_bar.png) | ![Studio Dark Analog](images/v100/studio_dark_analog.png) | ![Studio Dark Digital](images/v100/studio_dark_digital.png) |
| Warm Amber | ![Warm Amber Bar](images/v100/warm_amber_bar.png) | ![Warm Amber Analog](images/v100/warm_amber_analog.png) | ![Warm Amber Digital](images/v100/warm_amber_digital.png) |
| Classic Ivory | ![Classic Ivory Bar](images/v100/classic_ivory_bar.png) | ![Classic Ivory Analog](images/v100/classic_ivory_analog.png) | ![Classic Ivory Digital](images/v100/classic_ivory_digital.png) |


화면에서 양쪽 채널의 `RMS`, `Peak`, `Crest`와 `LUFS-M`, `LUFS-S`, `LUFS-I`, `LRA (prelim.)`를 확인할 수 있습니다. 상단의 **100ms RMS / Peak / Crest** 및 하단의 **DSD reconstructed signal** 문구는 촬영 화면에 나온 표기입니다. 여기서 `DSD reconstructed signal`은 **계측 화면의 신호 표기**이며 PCM 오디오 출력으로 변경됐다는 의미로 해석하지 않습니다. `LRA (prelim.)`는 잠정값 표시로 기록하며 최종 인증값으로 소개하지 않습니다.

수치들은 실제 촬영 시점의 예시로서 프로그램의 측정 정확도 인증·기준 음압·보정값을 나타내지 않습니다. 테마별 색상과 표시 방식의 차이를 보여주기 위한 화면입니다.

## 6. 사용 목적별 주요 설정 안내

| 원하는 동작 | 메뉴 위치 | 선택 가능한 항목 |
|---|---|---|
| 두 채널 동시 표시 | Layout | Left + Right (Horizontal / Vertical) |
| 한 채널만 확대해 표시 | Layout | Left Only / Right Only |
| 크기 조절 시 비율 고정 | Layout | Lock Aspect Ratio |
| 표시 레벨 선택 | Levels | RMS + Peak / RMS / Peak |
| 바늘 움직임 조절 | Movement | No Inertia / Curve Fit / Spring-Mass-Damper |
| 감쇠 속도 조절 | Decay | Fast / Normal (350 ms) / Slow (900 ms) / Custom |
| 상세 움직임 보정 | Tuning | Rise, Decay Custom, Peak Hold, Spring Speed, Spring Damping |
| 형식·진단 표시 | Options | Show PCM/DSD Format / Show FPS / Show Console Logs |
| 창 동작 | Options | Always on Top / Design Mode / Reset Options to Defaults |

이는 메뉴에 나타난 조작 방법을 정리한 표입니다. 녹화된 화면의 체크 상태를 전역 기본값으로 간주하지 않습니다.

**참고 — 화면과 레벨 스케일:** PCM/DSD에 따라 별도 배경을 선택하도록 스킨이 구성되어 있으며, 프로젝트에서 정한 경고 구간 기준은 PCM의 경우 0 dB부터, DSD의 경우 +3.1 dB부터입니다. 형식 전환 시 실제 눈금이 적용되는 모습은 별도 런타임 화면으로 확인할 항목입니다.

## 7. 설치 파일과 구성 (빌드 검증 기준)

### x86(32비트) 정식 빌드 및 재생 확인

2026-10-23 x86 / Win32 Release 빌드가 MSVC v145로 성공했습니다(오류 0개, 경고 10개). DLL SHA256은 `1C8E5C9D9CEAB8BA84AD162FB200A14E3DFC5C0FDC35549395813226C1AB109D`입니다. `.fb2k-component` 및 onedir ZIP 각각 DLL 1개 + 스킨 리소스 98개, 총 99개 파일 검사를 통과했습니다.

실제 **foobar2000 2.25.8 x86** 환경에서 `PCM/DSD VU 1.0.0` 컴포넌트 등록 및 독립 VU 창 실행을 확인했습니다. 사용자가 PCM과 DoP/DSD 음악 재생에서도 정상 작동함을 직접 확인했습니다.

![x86 Components: PCM/DSD VU 1.0.0](images/v100/components_x86_v100.png)

![foobar2000 x86 with PCM/DSD VU window](images/v100/x86_foobar_running.png)

2026-10-23 x64 Release 빌드에서 다음 패키지가 생성됐으며, x86도 동일한 구성으로 별도 빌드했습니다. foobar2000의 실제 아키텍처와 일치하는 패키지를 설치하십시오.

- `foo_pcm_dsd_vu.dll` — x64, 226,304바이트.
- `foo_pcm_dsd_vu_v1.0.0_x64.fb2k-component` — DLL 1개와 98개 리소스로 구성된 99개 파일 패키지.
- `PCM_DSD_VU_v1.0.0_x64.zip` — onedir 멀티파일 배포 ZIP(99개 파일).
- `foo_pcm_dsd_vu_v1.0.0_x86.fb2k-component` — x86용 99개 파일 설치 패키지.
- `PCM_DSD_VU_v1.0.0_x86.zip` — x86용 onedir 멀티파일 ZIP(99개 파일).

**설치 확인:** foobar2000을 종료하고 `.fb2k-component`를 설치한 뒤 재실행하여 `Preferences → Components`에서 `PCM/DSD VU / 1.0.0`을 확인합니다. 실제 설치 캡처에서 해당 이름과 버전이 확인됐습니다.

### 실제 설치 버전 확인

![foobar2000 Components — PCM/DSD VU 1.0.0](images/v100/components_v100.png)

*그림. foobar2000 2.25.8의 Components 목록에 `PCM/DSD VU` / `1.0.0` / `foo_pcm_dsd_vu`가 표시된 실제 사용자 캡처.*



## 8. 설치 후 점검과 문제 해결

- **Components에 이전 beta 버전이 보일 때:** 사용 중인 foobar2000 인스턴스에 v1.0.0 패키지가 적용됐는지 확인하고, 완전히 종료 후 재실행합니다.
- **VU 실행 메뉴가 보이지 않을 때:** 실제 사용 중인 foobar2000 인스턴스의 `Preferences → Components`에서 `foo_pcm_dsd_vu`의 설치 상태와 버전을 먼저 확인합니다.
- **PCM/DSD 형식 표시가 필요할 때:** 우클릭 `Options → Show PCM/DSD Format`을 확인합니다. 표시가 꺼져 있다는 사실만으로 신호 판별 실패라고 판단하지 않습니다.
- **바늘이 움직이지 않을 때:** 먼저 음원 재생과 실제 캡처 신호 유무를 확인합니다. 디자인 상태와 Level/Movement 설정도 확인 대상입니다. 이 항목들은 일반적인 확인 순서이며, 현재 자료에서 특정 장애 원인으로 확정한 것은 아닙니다.
- **기존 설치를 교체할 때:** 여러 foobar2000 Portable 설치본을 혼동하지 않고 TEST에서 검증한 뒤 실사용 환경에 적용합니다.

## 9. 검증 범위와 기술적 주의사항

- **설치 버전:** 실제 Components 스크린샷에서 `1.0.0` 확인 완료.
- **수치 표시:** RMS/Peak/Crest, LUFS-M/S/I, LRA (prelim.)의 실제 계측 화면 확보. Format/FPS 표시 토글의 개별 실행 상태는 별개입니다.
- **스킨 구성:** 24개 `.vusk`와 48개 형식별 PNG는 STEP25 목록에서 확인. 메뉴 전체 명칭·정렬은 해당 스크린샷에 모두 노출되지는 않습니다.
- **기술 사양:** 측정 계산식, Native DSD 입력 지원, 처리 가능 배수·샘플링 범위, DSP/출력 신호 비간섭 여부, 설정 저장 범위, 확인하지 않은 추가 플랫폼 지원은 주장하지 않음.

**문서 범위:** 실제 UI와 사용자 확인 사항을 기록합니다. 일부 기술 세부 사양은 별도 코드·계측 검증 전까지 수치로 주장하지 않습니다.
