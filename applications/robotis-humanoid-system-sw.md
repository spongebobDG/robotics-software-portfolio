# 로보티즈 휴머노이드 시스템 소프트웨어 엔지니어 지원 매핑

지원 공고: [휴머노이드 시스템 소프트웨어 엔지니어](https://robotisrecruiter.ninehire.site/job_posting/aE8A4gYI)

## 요구사항 대응표

| 공고 요구사항 | 현재 증거 | 판단 |
|---|---|---|
| ROS 2 기반 시스템 소프트웨어 | TurtleBot Fleet Ops의 bringup, Nav2, TF2, task lifecycle, watchdog | 강점 |
| C++ 또는 Python | C++ safety watchdog, Python ROS 2 agent·gateway·vision 모듈 | 강점 |
| Linux 개발·디버깅 | LDS-02 UART 무수신, 장치 소유권, RMW·Zenoh, Nav2 장애 분석 | 강점 |
| 센서·제어기 하드웨어 연동 | LDS-02, OpenCR, Raspberry Pi, ESP32, RGB/열화상 카메라 | 강점 |
| 실 로봇 시스템 이슈 분석 | 센서 TX 단선, 센서 축 180° 불일치, 통신 단절 안전 정지 | 강점 |
| 모바일 로봇·매니퓰레이터 | TurtleBot3 Burger, 서브 차량, 4축 감시 로봇암 | 보유 |
| DYNAMIXEL SDK | TurtleBot3 내부 사용 경험은 있으나 SDK 직접 구현 증거 없음 | 보완 필요 |
| ros2_control hardware interface | 팀 시스템의 `gz_ros2_control`은 개인 기여가 아님 | 보완 필요 |

## 면접에서 우선 설명할 사례

1. **센서 문제를 ROS 설정 문제가 아닌 물리 계층으로 좁힌 과정**
   - `/scan` publisher는 존재하지만 메시지가 없던 상황
   - 포트 read counter와 원시 UART를 확인해 LDS-02 TX 커넥터 이탈을 발견
   - 5초 동안 44,105 bytes와 패킷 헤더 940개를 확인한 뒤 드라이버 경로 복구
2. **네트워크 단절 시 로봇이 다시 움직이지 않도록 만든 안전 정책**
   - deadman, gateway, Zenoh 단절에서 최종 0 명령과 미재무장을 검증
   - 측정된 정지 경로는 0.301–0.305초
3. **센서 좌표계 계약을 실측으로 검증한 과정**
   - LDS-02 원본 전방이 물리 전방과 180° 어긋나는 문제를 발견
   - Nav2와 웹 overlay에 동일한 π rad 정규화를 적용

## 과장하지 않을 범위

- AIP Swarm의 `gz_ros2_control` 설정과 초기화 문제 해결은 개인 성과로 주장하지 않습니다.
- RobotOps Dashboard의 로봇 상태는 mock이며 실기기 관제 결과로 표현하지 않습니다.
- DYNAMIXEL SDK와 `ros2_control`은 신규 프로젝트에서 직접 구현·검증한 뒤에만 보유 역량으로 변경합니다.

## 다음 보완 프로젝트의 완료 기준

- 두 TurtleBot3의 실제 DYNAMIXEL/OpenCR 제어 경로와 충돌하지 않는 실험 구성을 먼저 확정
- SDK 통신, 상태 read, 명령 write, timeout, 오류 복구를 자동 테스트와 실기기 로그로 검증
- `ros2_control` command/state interface와 controller lifecycle을 직접 구현하거나 독립 실험 패키지로 재현
- 안전 정지 시간과 반복 실험 성공률을 측정
