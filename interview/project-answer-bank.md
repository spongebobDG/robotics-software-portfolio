# 프로젝트별 면접 답변 은행

문장을 그대로 암기하기보다 굵은 흐름과 검증 수치만 기억합니다. 면접관이 관심을 보이는 지점에서 코드·로그·한계로 내려갑니다.

## 1. TurtleBot Fleet Ops

원본: [turtlebot-fleet-ops](https://github.com/spongebobDG/turtlebot-fleet-ops)

### 30초 소개

“TurtleBot3를 단순히 주행시키는 데서 끝내지 않고, ROS 2 bring-up부터 Nav2 작업, 웹 관제, 네트워크 단절 시 안전 정지, 장애 복구까지 하나의 운영 가능한 시스템으로 묶은 프로젝트입니다. 대표 실기기 검증은 TB1에서 수행했으며, LDS-02 UART 장애를 물리 계층까지 내려가 해결했고 단절 후 최종 정지 경로를 0.301~0.305초로 측정했습니다.”

### 3분 설명 흐름

1. **문제 정의:** 두 대 운영을 목표로 했지만 우선 한 대의 bring-up·안전·복구 경로를 실기기에서 완성해야 했습니다.
2. **구조:** TurtleBot3/OpenCR/LDS-02 → ROS 2 agent·Nav2 → gateway·Zenoh → 웹 관제 순서로 설명합니다.
3. **핵심 구현:** bring-up, 작업 lifecycle, deadman·e-stop·watchdog, 장애 진단 문서화를 설명합니다.
4. **장애 사례:** `/scan` publisher는 있지만 메시지가 없던 문제를 UART byte와 header 수로 검증해 LDS-02 TX 연결 문제로 좁혔습니다.
5. **검증:** 5초간 44,105 bytes와 header 940개, 정지 경로 0.301~0.305초, 600초 순찰 11 loops·fault 0을 제시합니다.
6. **한계:** TB2 자동 할당과 전체 2대 실기기 acceptance는 완료 범위가 아니며, SDK 직접 제어 프로젝트도 아닙니다.

### 장애 해결 답변

“처음에는 ROS 2 QoS나 driver parameter를 의심할 수 있었지만 publisher 자체가 살아 있었기 때문에 센서 입력 경로를 분리했습니다. 포트 read counter와 raw UART를 확인하니 데이터가 없었고, 배선과 전원을 다시 추적해 LDS-02 TX 연결 이탈을 찾았습니다. 복구 후 5초간 44,105 bytes와 header 940개를 확인하고 `/scan`까지 이어지는 경로를 검증했습니다. 이 경험으로 로봇 장애는 노드 설정부터 보지 않고 물리 입력, driver, ROS graph 순으로 계층을 나눠 확인해야 한다는 기준을 만들었습니다.”

### 본인 기여 경계

- 직접 수행: 전체 MVP 설계·구현, bring-up, 안전 정책, 관제·작업 경로, 실기기 검증
- 미완료: TB2 자동 할당, 2대 전체 acceptance
- 보유하지 않은 경험: DYNAMIXEL SDK 직접 구현, `ros2_control` hardware interface 구현

### 예상 후속 질문

- 정지 시간이 왜 약 0.3초인가?
- deadman, gateway, Zenoh 중 어느 계층이 최종 안전 책임을 갖는가?
- DDS와 Zenoh를 함께 쓴 이유와 장애 격리 방법은?
- LiDAR 좌표 보정을 Nav2와 odometry에 각각 어떻게 반영했는가?

## 2. AIP Swarm Case Study

공개 문서: [aip-swarm-case-study](https://github.com/spongebobDG/aip-swarm-case-study)

### 30초 소개

“ROS 2 군집 시스템 전체를 개인 성과로 주장하지 않고, 제가 맡은 카메라 비전, 웹 관제, 서브 차량 구동이 팀 ROS graph와 만나는 인터페이스를 중심으로 정리한 팀 프로젝트입니다. 공개 case study에는 본인 수행, 공동 수행, 팀 시스템을 분리해 기여 범위를 명확히 표시했습니다.”

### 3분 설명 흐름

1. **팀 목표:** 여러 차량의 상태·카메라 정보를 중앙에서 확인하고 명령을 전달하는 군집 시스템이었습니다.
2. **본인 담당:** 카메라·인식 결과 경로, 웹 관제 서버·화면, 서브 차량 구동 연동입니다.
3. **인터페이스:** perception 결과와 차량 상태가 관제에 들어오고, 관제 명령이 서브 차량 구동 경로로 내려가는 흐름을 설명합니다.
4. **협업:** launch/config와 메시지 인터페이스를 팀원 구현과 맞추고 통합 시험한 과정을 설명합니다.
5. **기여 증명:** 공용 `AIP Team` 저자 커밋 수를 개인 지표로 사용하지 않고 담당 코드와 역할 표로 설명합니다.
6. **한계:** Gazebo, Nav2 전체 구성과 `gz_ros2_control` 문제 해결은 팀 시스템이며 개인 구현으로 주장하지 않습니다.

### 협업 장애 답변

“팀 프로젝트에서는 기능 자체보다 인터페이스 경계가 자주 문제였습니다. 저는 카메라·관제·서브 차량 경로에서 입력과 출력 메시지를 먼저 고정하고, launch/config 변경이 생기면 담당자와 함께 통합 경로를 다시 확인했습니다. 면접에서는 팀 전체 결과를 제 성과로 넓히지 않고, 제가 설명할 수 있는 코드와 연결 지점만 답하겠습니다.”

### 본인 기여 경계

- 직접 수행: 카메라 비전, 웹 관제, 서브 차량 구동 연동
- 공동 수행: 팀 ROS 2 graph와의 인터페이스 조율·통합 시험
- 팀 시스템: Gazebo world, Nav2 전체 구성, `gz_ros2_control`

### 예상 후속 질문

- 카메라 결과와 관제 상태의 메시지 계약은 어떻게 정했는가?
- 여러 차량의 namespace와 topic 충돌을 어떻게 피했는가?
- 개인 기여를 코드 단위로 어디까지 설명할 수 있는가?

## 3. Industrial Robot Arm Vision

원본: [aip_robotarm_vision](https://github.com/spongebobDG/aip_robotarm_vision)

### 30초 소개

“비전·기구학·상태 머신은 Raspberry Pi가 담당하고, 안전한 50 Hz 서보 구동은 ESP32가 담당하도록 분리한 4축 감시 로봇팔 프로젝트입니다. Wi-Fi가 끊겨도 마지막 명령이 계속 유지되지 않도록 watchdog을 두었고, 명령 중단 시험에서 세 번 모두 8초 후 자동 relax되는 것을 확인했습니다.”

### 3분 설명 흐름

1. **분리 이유:** 영상 처리 지연이 모션 제어 주기를 직접 흔들지 않도록 Pi와 ESP32의 책임을 분리했습니다.
2. **데이터 흐름:** RGB/열화상 → Pi vision·fusion·FSM → MQTT setpoint → ESP32 50 Hz interpolation → servo입니다.
3. **안전:** 도달 불가능 목표 거부, servo 범위 제한, watchdog, 종료 시 HOME/RELAX 정책을 설명합니다.
4. **검증:** 5분 18초 동안 `arm/state` 1,581건, 1초 이상 gap 0건, watchdog 3회 성공을 제시합니다.
5. **기구학·비전:** FK↔IK 4자세 최대 오차 0.00°, RGB 약 23 FPS, RGB–열화상 affine 보정을 설명합니다.
6. **한계:** 전체 감시 시나리오 장시간 acceptance와 정밀한 카메라·기구 캘리브레이션은 후속 검증이 필요합니다.

### 안전 설계 답변

“MQTT 연결이 끊겼을 때 마지막 setpoint를 계속 유지하면 위험할 수 있습니다. 그래서 ESP32가 마지막 유효 명령 시간을 독립적으로 감시하고 timeout이 지나면 relax하도록 했습니다. Pi 프로세스 상태와 무관하게 MCU가 최종 안전 동작을 수행하도록 책임을 분리했고, 명령 중단 시험 세 번에서 모두 8초 후 relax되는 것을 확인했습니다.”

### 본인 기여 경계

- 직접 수행: Pi–ESP32 인터페이스, FK/IK 제한, RGB·열화상 도구, FSM, watchdog·종료 정책
- 아직 부족: 장시간 전체 시나리오 acceptance, 정밀 캘리브레이션 오차 보고서

### 예상 후속 질문

- watchdog을 8초로 둔 이유와 더 짧게 만들 때의 trade-off는?
- MQTT를 선택한 이유와 ROS 2 통신으로 바꿀 때 달라지는 점은?
- servo interpolation과 명령 제한은 어디에서 책임지는가?

## 4. Camping Safe Guard

원본: [Camping-Safe-Guard](https://github.com/spongebobDG/Camping-Safe-Guard)

### 30초 소개

“MQ-9·온습도 센서, ESP32 추론, 무선 전달, 사용자 화면과 3D 프린팅 케이스까지 통합한 캡스톤 프로젝트입니다. KCC 학술대회 논문 심사를 통과해 poster session에서 발표했으며, 센서부터 TinyML·하드웨어까지 연결한 경험을 보여줍니다.”

### 3분 설명 흐름

1. 캠핑 환경의 일산화탄소·환경 이상 감지 문제를 정의합니다.
2. 센서 calibration → feature/window → TFLite Micro inference → 무선 전달 → 화면 흐름을 설명합니다.
3. MCU 메모리와 전력 제약 속에서 sliding buffer와 추론 경로를 구성한 이유를 설명합니다.
4. 케이스와 배터리 배치를 포함한 하드웨어 통합 경험을 설명합니다.
5. KCC 심사 통과와 poster 발표 사실을 제시합니다.
6. 정확도·추론 시간·메모리 사용량의 재현 가능한 보고가 아직 부족하다는 한계를 먼저 밝힙니다.

### 본인 기여 경계

면접 전 캡스톤 팀 내 정확한 개인 역할을 한 문장으로 확정합니다. 저장소에서 직접 설명할 수 없는 팀원의 구현을 개인 성과로 포함하지 않습니다.

### 예상 후속 질문

- MQ-9 calibration과 PPM 환산의 한계는?
- TinyML 모델을 선택한 기준과 MCU 메모리 제약은?
- 경보 오탐과 미탐 중 무엇을 더 위험하게 보았는가?

## 5. ROS2 RobotOps Dashboard

원본: [ros2-robotops-dashboard](https://github.com/spongebobDG/ros2-robotops-dashboard)

### 30초 소개

“실기기 제어 성과가 아니라 로봇 로그 진단과 운영 스택을 로컬에서 재현하기 위해 만든 보조 프로젝트입니다. FastAPI, WebSocket, MLflow, Prometheus, Grafana를 연결했고 pytest 46건을 통과했지만, 데이터와 성능 수치는 합성·mock임을 명확히 표시합니다.”

### 3분 설명 흐름

1. 로봇 상태와 장애 로그를 한 화면에서 추적하는 문제를 설명합니다.
2. API·WebSocket·분류 모델·모니터링 스택의 역할을 설명합니다.
3. pytest 46건과 Docker Compose 재현 경로를 제시합니다.
4. accuracy/macro F1 1.00이 명확히 분리된 합성 데이터 결과라 일반화 성능이 아님을 설명합니다.
5. 로봇 제어 핵심 프로젝트가 아닌 진단·백엔드 보조 역량으로만 배치한 이유를 설명합니다.

### 예상 후속 질문

- mock 데이터를 실제 rosbag·로그로 바꾸려면 무엇이 필요한가?
- 모델 성능보다 운영 신뢰성을 어떤 지표로 평가하겠는가?
- WebSocket 재연결과 데이터 유실을 어떻게 처리할 것인가?
