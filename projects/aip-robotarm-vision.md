# Industrial Robot Arm Vision

원본 저장소: [spongebobDG/aip_robotarm_vision](https://github.com/spongebobDG/aip_robotarm_vision)

## 해결하려던 문제

Raspberry Pi가 비전·기구학·상태 머신을 담당하고 ESP32가 4축 MG996R 서보를 50 Hz로 제어하는 분산 감시 로봇암을 구축했습니다.

## 시스템과 데이터 흐름

`RGB/열화상 → Pi vision·fusion·FSM → MQTT setpoint → ESP32 50 Hz interpolation → 4축 servo`

## 본인 기여

- Pi–ESP32 MQTT 명령·상태 인터페이스
- FK/IK와 도달 불가능 목표 거부
- RGB·열화상 수집, 보정, 융합 도구
- 감시 FSM, 추적기, watchdog과 종료 시 HOME/RELAX 정책

## 검증 결과

- 4축 조그 5분 18초 동안 `arm/state` **1,581건**, 1초 이상 telemetry gap 0건
- 명령 중단 3회 모두 마지막 명령 후 **8초**에 자동 `relaxed`
- 4개 자세 FK→IK round-trip 오차 **0.00°** 및 도달 불가능 목표 reject
- RGB 카메라 640×480 약 **23 FPS**
- RGB–열화상 affine: scale 약 0.90, rotation 약 3.8°, translation +26.7/+17.5 px
- 공개 placeholder 설정으로 PlatformIO build 성공: RAM 13.8%, flash 58.8%

## 한계

- Phase 4 감시 코드가 구현되어 있지만 전체 시나리오의 장시간 실기기 acceptance 결과는 아직 문서화되지 않았습니다.
- 아날로그 서보와 단순 2-link 모델의 정밀도 한계가 있습니다.

## 면접 답변

- **30초:** “비전과 고수준 판단은 Pi, 안전한 50 Hz 구동은 ESP32에 분리해 Wi-Fi 지터가 모션 제어 주기에 직접 영향을 주지 않도록 설계했습니다.”
