# ROBOTIS 면접 준비

목표 직무는 **휴머노이드 시스템 소프트웨어 엔지니어**이며, 답변의 중심은 설치·운영이 아니라 **ROS 2 로봇 시스템 소프트웨어를 직접 설계하고 디버깅한 경험**입니다.

> English positioning: ROS 2 robot systems software developer focused on hardware integration, safe control, perception, and reproducible debugging.

## 10초 포지셔닝

“저는 ROS 2에서 센서·제어기·네트워크를 연결하고, 실기기 장애를 로그와 측정값으로 좁혀 안전하게 복구하는 로봇 시스템 소프트웨어 개발자입니다.”

## 60초 자기소개

“안녕하세요. ROS 2 로봇 시스템 소프트웨어 개발자를 목표로 하는 김대건입니다. TurtleBot3 실기기 프로젝트에서 OpenCR과 LDS-02를 bring-up하고 Nav2, 작업 제어, 안전 정지와 장애 복구 경로를 구현했습니다. 특히 `/scan`이 발행되지 않던 문제를 ROS 설정만 바꾸지 않고 raw UART 수신량을 확인해 물리 TX 연결 문제로 좁혔고, 네트워크 단절 시에는 약 0.3초 안에 최종 정지 명령이 전달되는 것을 반복 측정했습니다. 팀 군집 프로젝트에서는 카메라 비전, 웹 관제, 서브 차량 구동을 맡았으며 팀 시스템과 개인 기여를 구분해 설명합니다. 아직 DYNAMIXEL SDK 직접 제어와 `ros2_control` hardware interface 경험은 부족하므로, 두 대의 TurtleBot3를 활용한 실기기 제어 프로젝트로 보완할 계획입니다. 로보티즈에서 하드웨어와 맞닿는 ROS 2 시스템을 안정적으로 개발하고 싶습니다.”

## 답변 우선순위

1. **TurtleBot Fleet Ops** — ROS 2 실기기 통합, Linux 디버깅, 안전 정지
2. **AIP Swarm Case Study** — 팀 인터페이스, 카메라 비전, 웹 관제, 서브 차량
3. **Industrial Robot Arm Vision** — Pi–ESP32 분산 제어, watchdog, 비전·기구학
4. **Camping Safe Guard** — 센서·TinyML·임베디드 통합, KCC poster
5. **RobotOps Dashboard** — mock 기반 운영·진단 보조 역량

## 답변 구성 원칙

모든 기술 답변은 다음 순서로 말합니다.

1. **문제:** 어떤 실패 또는 요구사항이 있었는가
2. **가설:** 가능한 원인을 어떻게 나눴는가
3. **검증:** 어떤 로그·명령·측정값을 확인했는가
4. **조치:** 코드·배선·설정을 어떻게 바꿨는가
5. **결과:** 무엇으로 성공을 확인했는가
6. **한계:** 아직 검증하지 못한 것은 무엇인가

## 숫자를 말할 때의 규칙

- 수치를 먼저 외우지 말고 **측정 조건과 의미**를 함께 기억합니다.
- 팀 결과와 개인 결과를 분리합니다.
- mock 데이터 성능을 실기기 성능처럼 표현하지 않습니다.
- `DYNAMIXEL SDK`와 `ros2_control`은 직접 구현 전까지 “학습·보완 중”으로 답합니다.

## 관련 문서

- [프로젝트별 답변 은행](project-answer-bank.md)
- [ROBOTIS 질문 은행](robotis-question-bank.md)
- [직무 요구사항 대응표](../applications/robotis-humanoid-system-sw.md)
- [제출 체크리스트](../applications/submission-checklist.md)
