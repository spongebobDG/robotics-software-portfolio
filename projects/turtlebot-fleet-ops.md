# TurtleBot Fleet Ops

원본 저장소: [spongebobDG/turtlebot-fleet-ops](https://github.com/spongebobDG/turtlebot-fleet-ops)

## 해결하려던 문제

TurtleBot3 한 대를 단순히 움직이는 수준을 넘어 bringup, 상태 수집, 웹 관제, Nav2 작업, 안전 정지, 장애 복구까지 하나의 운영 가능한 ROS 2 시스템으로 연결했습니다.

## 시스템과 기술

- TurtleBot3 Burger, Raspberry Pi 4, OpenCR, LDS-02
- Ubuntu 22.04, ROS 2 Humble, Nav2, TF2, Zenoh
- Python agent·gateway, C++ watchdog, FastAPI·Web UI

## 본인 기여

- 전체 단일 로봇 MVP의 설계·구현·실기기 검증
- OpenCR·LiDAR bringup 및 장치·UART 디버깅
- deadman, e-stop, watchdog, 미재무장 정책
- 지도·순찰·작업 lifecycle과 장애 진단 문서화

## 핵심 장애 해결

`/scan` publisher는 존재하지만 데이터가 없었습니다. ROS 파라미터를 반복 변경하지 않고 포트 read counter와 원시 UART를 확인해 물리 계층으로 범위를 좁혔고, LDS-02 TX 커넥터 이탈을 발견했습니다. Raspberry Pi UART 경로에서 5초간 44,105 bytes와 헤더 940개를 확인한 뒤 `/scan`을 복구했습니다.

## 검증 결과

- deadman·Gateway·Zenoh 단절 후 최종 0 명령: **0.301–0.305초**, 자동 재개 없음
- 600초 순찰: **11 loops**, CPU 66.1–73.6%, memory 27.1–27.3%, fault 0
- 센서 축 보정 후 수동 전진: map projection `+0.0349 m`, odometry `+0.0422 m`
- JavaScript helper 자동 테스트 29건 통과 및 GitHub Actions ROS 2 CI 운영

## 한계

- 대표 실기기 검증은 TB1 한 대이며 TB2 자동 할당은 완료 범위가 아닙니다.
- OpenCR 내부 DYNAMIXEL 제어를 사용하지만 DYNAMIXEL SDK를 직접 구현한 프로젝트는 아닙니다.

## 면접 답변

- **30초:** “TurtleBot3를 ROS 2에서 bringup하고 끝내지 않고, 센서·Nav2·웹 관제·안전 정지·복구까지 실제 로봇에서 검증한 프로젝트입니다.”
- **3분 핵심:** LDS-02 무수신 원인 분리 → 물리 TX 문제 발견 → UART 정량 검증 → 최소 변경으로 복구 → 회귀 방지 문서화.
