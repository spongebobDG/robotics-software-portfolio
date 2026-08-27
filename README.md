# 김대건 | ROBOTIS 휴머노이드 시스템 소프트웨어 지원 포트폴리오

ROS 2 실기기 통합, 안전 제어, 임베디드와 비전 기반 로봇 시스템 프로젝트를 **문제 → 판단 → 구현 → 검증 → 한계** 순서로 정리했습니다.

> 목표 직무: [로보티즈 휴머노이드 시스템 소프트웨어 엔지니어](https://robotisrecruiter.ninehire.site/job_posting/aE8A4gYI)<br>
> 핵심 관점: 로봇을 움직이는 코드보다, 현실의 변수 속에서도 안전하게 동작하는 시스템

## 30초 요약

| 프로젝트 | 역할·성과 | 대표 근거 | 직무 연결 |
|---|---|---|---|
| [TurtleBot Fleet Ops](projects/turtlebot-fleet-ops.md) | 개인 · AI 부트캠프 우수상 | 0.301–0.305초 단절 정지, 600초 11 loops, LiDAR 9단계 추적 | ROS 2, Linux 디버깅, 센서·제어기 연동 |
| [Camping Safe Guard](projects/camping-safe-guard.md) | 4인 팀장 · KCC 2026 제1저자 | 174KB LSTM → 약 10KB 1D-CNN, ESP-NOW, 하이브리드 안전 판단 | MCU 펌웨어, 센서, 통신, 엣지 AI |
| [Dobot Vision Sorter](projects/dobot-vision-sorter.md) | 개인 | 실기기 64.7초 데모, held-out 보정 검증, 12 tests | 매니퓰레이터, 좌표 변환, 명령 안전 가드 |
| [Industrial Robot Arm Vision](projects/aip-robotarm-vision.md) | 개인 | 50 Hz 로컬 제어, 8초 relax, FK→IK 0.00° | 분산 제어, watchdog, 비전·기구학 |
| [AIP Swarm](projects/aip-swarm.md) | 5인 팀 · 담당 범위 명시 | Docker sim 3대, supervisor/simulation 56 tests | ROS 2 통신 계약, 관제, 팀 통합 |

## 포트폴리오에서 반복한 설계 원칙

1. **상위 판단과 하위 안전 계층을 분리합니다.** AI가 틀리거나 네트워크가 끊겨도 로봇이 위험한 명령을 유지하지 않게 합니다.
2. **오류를 숨겨 동작시키지 않습니다.** 범위 밖 좌표와 정합률 미달 pose는 보정된 것처럼 만들지 않고 거부합니다.
3. **계층별로 장애 범위를 좁힙니다.** ROS 2 토픽에서 시작해 프로세스, 장치, UART와 배선까지 내려갑니다.
4. **증거 수준을 구분합니다.** 실기기, simulation, HIL과 mock 결과를 같은 완료 상태로 표시하지 않습니다.
5. **팀 성과와 개인 기여를 분리합니다.** AIP Swarm은 담당 기능과 팀 시스템의 경계를 별도 case study에 공개했습니다.

## ROBOTIS 직무 대응

| 채용 요구사항 | 현재 근거 |
|---|---|
| ROS 2 기반 시스템 소프트웨어 | TurtleBot bringup·SLAM·Nav2·task lifecycle·안전 정지 |
| C++ 또는 Python | C++ safety watchdog 적용·검증, Python ROS 2 agent·gateway·vision |
| Linux 개발·디버깅 | `/scan` 무수신, UART, 장치 소유권, RMW·Zenoh 장애 추적 |
| 로봇 하드웨어 연동 | OpenCR·LDS-02·Raspberry Pi·ESP32·Dobot·RGB/열화상 센서 |
| 실 로봇 시스템 이슈 개선 | 센서 TX 이탈, 축 180° 불일치, 통신 단절, 좌표 보정 실패 처리 |
| DYNAMIXEL SDK · `ros2_control` | 문서·코드 학습 중이며 직접 실기기 구현 증거는 아직 없음 |

상세 대응과 면접 우선 사례는 [ROBOTIS 지원 매핑](applications/robotis-humanoid-system-sw.md)에 정리했습니다.

## 먼저 볼 순서

1. [TurtleBot Fleet Ops — 대표 프로젝트](projects/turtlebot-fleet-ops.md)
2. [LiDAR `/scan` 무수신 9단계 추적](https://github.com/spongebobDG/turtlebot-fleet-ops/blob/main/docs/case-studies/lds02-scan-data-recovery.md)
3. [Camping Safe Guard — MCU 제약과 안전 판단](projects/camping-safe-guard.md)
4. [Dobot Vision Sorter — 좌표 변환과 fail-fast 제어](projects/dobot-vision-sorter.md)
5. [AIP Swarm — 개인 기여와 팀 시스템 경계](projects/aip-swarm-case-study.md)

## 현재 학습 과제

OpenCR을 통해 DYNAMIXEL을 운용한 경험은 있지만, DYNAMIXEL SDK 직접 제어와 `ros2_control` hardware interface를 실기기에서 구현·검증한 증거는 아직 없습니다. Protocol 2.0, Control Table, Sync Write/Bulk Read와 `SystemInterface` lifecycle을 의존 순서대로 학습하고 있습니다. 완료 전까지는 보유 역량으로 표시하지 않습니다.

<details>
<summary>이전 포트폴리오 허브 내용 보존</summary>

# 김대건 | ROS 2 Robot Systems Software Developer

ROS 2 기반 로봇 시스템을 실제 하드웨어에서 통합하고, 센서·통신·제어 문제를 로그와 측정값으로 분석하는 소프트웨어 개발자 포트폴리오입니다.

> I build and debug ROS 2 robot systems across hardware integration, safe motion, perception, and fleet operations. Every claim below is limited to work I implemented or can support with code, logs, or test evidence.

## Target Role

- 1순위: [로보티즈 휴머노이드 시스템 소프트웨어 엔지니어](https://robotisrecruiter.ninehire.site/job_posting/aE8A4gYI)
- 장기 방향: ROS 2 제어, 모바일 로봇, 매니퓰레이터, 퍼셉션 시스템 소프트웨어 개발
- 관심 밖 직무: 설치·운영·필드 지원 중심 직무

## What I Build

- **ROS 2 robot software:** Humble, Nav2, TF2, lifecycle/task control, watchdog
- **Hardware integration:** TurtleBot3 Burger, OpenCR, LDS-02, Raspberry Pi, ESP32
- **Perception:** RGB/thermal vision, camera calibration, tracking, TinyML
- **Operations:** fleet monitoring, fault diagnosis, reproducible tests and deployment

## Top 3 Evidence

| Project | What it proves | Evidence |
|---|---|---|
| [TurtleBot Fleet Ops](https://github.com/spongebobDG/turtlebot-fleet-ops) | ROS 2 실기기 통합, Nav2, 안전 제어, Linux 디버깅 | LDS-02 UART 복구, 0.301–0.305초 단절 정지, 600초 순찰 |
| [AIP Swarm Case Study](https://github.com/spongebobDG/aip-swarm-case-study) | 팀 환경에서 카메라 비전·웹 관제·서브 차량 구동 | 역할·비소유 영역을 분리한 contribution matrix |
| [Industrial Robot Arm Vision](https://github.com/spongebobDG/aip_robotarm_vision) | Pi–ESP32 분산 제어, 4축 안전 제어, RGB/열화상 융합 | 50 Hz 제어, 8초 watchdog relax, RGB 약 23 FPS |

## Featured Projects

1. **[TurtleBot Fleet Ops](projects/turtlebot-fleet-ops.md)** — ROS 2 TurtleBot3 실기기 운영·안전·자율주행
2. **[AIP Swarm Case Study](projects/aip-swarm-case-study.md)** — 팀 프로젝트의 카메라 비전·웹 관제·서브 차량 구동
3. **[Industrial Robot Arm Vision](projects/aip-robotarm-vision.md)** — Raspberry Pi와 ESP32 기반 4축 감시 로봇암
4. **[Camping Safe Guard](projects/camping-safe-guard.md)** — ESP32 센서·TinyML 기반 캠핑 안전 시스템과 KCC poster 발표
5. **[ROS2 RobotOps Dashboard](projects/ros2-robotops-dashboard.md)** — mock 데이터 기반 로봇 관제·장애 진단 보조 프로젝트

직무 요구사항과 프로젝트의 연결은 [ROBOTIS 지원 매핑](applications/robotis-humanoid-system-sw.md)에 정리했습니다.

## Contribution Policy

- 팀 프로젝트는 `본인 수행`, `공동 수행`, `팀 시스템`을 구분합니다.
- 학습한 내용이더라도 과거에 직접 수행하지 않은 작업은 개인 기여로 표시하지 않습니다.
- mock·시뮬레이션·실기기 결과를 서로 바꿔 표현하지 않습니다.
- 성능 수치는 재현 절차, 로그 또는 저장소 문서로 확인 가능한 경우에만 사용합니다.

## Current Gap and Next Project

현재 포트폴리오에는 ROS 2와 실기기 통합 경험이 있지만 DYNAMIXEL SDK 기반 직접 제어와 `ros2_control` hardware interface 구현 증거가 부족합니다. 두 대의 TurtleBot3를 활용한 별도 실기기 프로젝트로 이를 보완하고, 검증이 끝나면 RobotOps Dashboard를 대표 목록에서 교체할 예정입니다.

## Contact

- GitHub: [@spongebobDG](https://github.com/spongebobDG)
- 프로젝트별 질문은 해당 저장소의 Issue에서 받을 수 있습니다.

</details>
