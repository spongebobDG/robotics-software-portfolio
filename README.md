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

## Interview Preparation

- [면접 준비 시작점](interview/README.md)
- [프로젝트별 30초·3분 답변](interview/project-answer-bank.md)
- [ROBOTIS 직무 질문·답변 은행](interview/robotis-question-bank.md)
- [지원서·GitHub 제출 체크리스트](applications/submission-checklist.md)

## Contact

- GitHub: [@spongebobDG](https://github.com/spongebobDG)
- 프로젝트별 질문은 해당 저장소의 Issue에서 받을 수 있습니다.
