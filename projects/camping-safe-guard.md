# Camping Safe Guard

원본 저장소: [spongebobDG/Camping-Safe-Guard](https://github.com/spongebobDG/Camping-Safe-Guard)

## 해결하려던 문제

캠핑 환경에서 일산화탄소와 온습도 상태를 감지하고, ESP32에서 위험도를 판단해 사용자에게 전달하는 임베디드 안전 시스템입니다.

## 시스템과 기술

- ESP32/ESP32-C3, MQ-9, DHT11, OLED
- ESP-NOW/BLE 기반 데이터 전달 실험
- TensorFlow Lite Micro 기반 TinyML 모델 실험
- 3D 프린팅 케이스와 배터리 승압 효율 자료

## 구현 근거

- MQ-9 센서 calibration과 CO PPM 판정 경로
- 온도·습도·가스 데이터를 포함하는 펌웨어 구조
- sliding input buffer와 TFLite Micro inference 코드
- 모바일 표시용 HTML 프로토타입

## 학술 성과

캡스톤 결과를 KCC 학술대회 논문으로 제출해 심사를 통과하고 poster session에서 발표했습니다. 논문 제목·저자·공식 프로그램 링크는 확인 가능한 원본 자료를 확보한 뒤 저장소에 추가합니다.

## 현재 한계

- 저장소에 실험 버전과 중복 폴더가 함께 있어 기준 firmware를 명확히 분리해야 합니다.
- 모델 정확도·추론 지연·메모리 사용량의 재현 가능한 평가 보고서가 아직 없습니다.
- 안전 장치는 보조 수단이며 상용 CO 경보기나 인증된 안전 설비를 대체하지 않습니다.

## 면접 답변

- **30초:** “센서 입력부터 MCU 추론, 무선 전달, 케이스 제작까지 연결한 캡스톤이며, 결과를 KCC poster session에서 발표했습니다.”
