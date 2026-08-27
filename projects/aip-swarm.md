# AIP Swarm

원본 저장소: [spongebobDG/aip-swarm-portfolio](https://github.com/spongebobDG/aip-swarm-portfolio)<br>
개인 기여 case study: [spongebobDG/aip-swarm-case-study](https://github.com/spongebobDG/aip-swarm-case-study)

## 프로젝트 범위

2026년 4월부터 6월까지 5인 팀으로 진행한 ROS 2 기반 산업 감시 로봇 관제 프로젝트입니다. 여러 차량의 상태와 지도·pose, RGB·열화상 결과를 중앙 PC에서 확인하고 수동 제어와 E-Stop 명령을 전달하는 시스템을 구성했습니다.

## 본인 담당

- 카메라·열화상 연동과 인식 결과 처리
- FastAPI·WebSocket 기반 웹 관제 화면 연결
- 서브차량 구동 흐름 정리와 ROS 2 인터페이스 통합
- 통신 계약 문서화와 시연 자료 준비

Nav2·SLAM 전체 설정, 일부 차량의 firmware와 실차 bringup은 팀 시스템이며 개인 구현으로 표시하지 않습니다.

## ROS 2 통신 계약

- 공통 메시지: `FleetHeartbeat`, `FleetStatus`, `OverrideCommand`, `PerceptionAlert`, `PeerPoseArray`
- 제어 우선순위: E-Stop → manual override → coordinator → Nav2
- `twist_mux`로 입력을 중재해 최종 `cmd_vel` 결정
- 차량 heartbeat 누락 시 supervisor/watchdog이 override 기반 E-Stop 요청

## 검증 상태

| 범위 | 상태 |
|---|---|
| Docker simulation | 3대 상태, 지도·pose, 데모 주행, supervisor/simulation **56 tests** 통과 |
| 실차 개별 구동 | 차량별 구동 확인 |
| 실차 3대 동시 장시간 군집 주행 | 미검증 |
| YOLO 현장 정확도·일부 서보 driver 완성도 | 추가 검증 필요 |

## 실패에서 배운 점

차량을 한 대씩 시험한 뒤 합치면 될 것이라고 판단했지만, 세 대가 영상을 동시에 전송하면서 무선 대역을 점유해 제어와 상태 전달까지 지연됐습니다. 다시 설계한다면 제어·상태와 영상 채널을 분리하고, 영상 해상도·프레임·발행 조건을 제한하며, 두 번째 차량을 붙이는 시점부터 통합 부하 시험을 진행하겠습니다.

## ROBOTIS 직무 연결

여러 모듈이 하나의 통신 자원을 공유할 때 개별 기능의 성공만으로 전체 시스템의 안정성을 보장할 수 없다는 점을 배웠습니다. 다관절 로봇에서도 축별 상태와 명령의 주기, 버스 대역과 실패 처리를 시스템 수준에서 확인하겠습니다.
