# ROS2 RobotOps Dashboard

원본 저장소: [spongebobDG/ros2-robotops-dashboard](https://github.com/spongebobDG/ros2-robotops-dashboard)

## 해결하려던 문제

ROS 2 장애 로그를 분류하고 로봇 상태를 웹에서 확인하는 운영 보조 시스템을 재현 가능한 로컬 환경으로 구성했습니다.

## 구현

- FastAPI REST·WebSocket API와 정적 대시보드
- TF-IDF + Logistic Regression 장애 로그 분류
- MLflow, Prometheus, Grafana, Docker Compose
- GitHub Actions CI·재학습 workflow

## 검증 결과

- pytest 46건 통과 기록
- mock 검증셋 accuracy/macro F1 1.00
- Docker Compose로 API, MLflow, Prometheus, Grafana 실행

## 반드시 구분할 점

- 데이터와 로봇 5대 상태는 **합성·mock 데이터**입니다.
- macro F1 1.00은 패턴이 분명한 합성 데이터의 결과이며 실환경 일반화 성능이 아닙니다.
- 로봇 제어 프로젝트가 아니라 관제·진단·운영 자동화 보조 역량을 보여주는 프로젝트입니다.

## 면접 답변

- **30초:** “실기기 성과로 포장하지 않고, 로봇 로그 진단과 운영 스택을 로컬에서 재현하기 위해 만든 mock 기반 보조 프로젝트입니다.”
