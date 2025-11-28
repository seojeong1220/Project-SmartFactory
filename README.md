<img width="1260" height="891" alt="Image" src="https://github.com/user-attachments/assets/600a07b7-64cd-4822-b122-ef01c0ea5cd6" />

# Intel Geti + AI QC Conveyor
인텔 Geti + 인공지능 QC 컨베이어


## 프로젝트 소개
공장 생산라인에서 병뚜껑의 QC 스티커 유무, 오염도 비율을 AI 모델이 자동 분석하고,
분류 결과에 따라 아두이노 기반 포토센서·액추에이터가 실시간으로 물체를 레일에서 자동 분류하는 스마트 팩토리 모형 시스템입니다.

또한, 버튼 하나로 Pink/Purple 모델을 한 라인에서 구별하는 유연한 생산 자동화 시스템을 구현했습니다.
<br>

## 개발 기간
* 25.09.24 - 25.10.22

### 개발 환경
- `Intel Geti`
- `Python 3.12.3`
- `Arduino Mega`
- `MariaDB 10`
- `Tkinter`

## 주요 기능
#### 모델 1 작동
- Pink 병뚜껑 QC 스티커 유무, 오염 유무
- No 스티커 or 오염 30% 초과 or Purple 병뚜껑 -> 완전불량
- 스티커 and 오염 0% 초과 30% 이하 -> 부분불량
- 스티커 and 오염 0% -> 정상

#### 모델 2 작동
- Purple 병뚜껑 QC 스티커 유무, 오염 유무
- No 스티커 or 오염 30% 초과 or Pink 병뚜껑 -> 완전불량
- 스티커 and 오염 0% 초과 30% 이하 -> 부분불량
- 스티커 and 오염 0% -> 정상

#### 관리자 모드
- 수동 컨베이어 제어
- 수동 엑츄에이터 조작

#### AI 모델 개발 과정 (요약)

- Detection: YOLOX-Tiny
- Segmentation: SegNext-S
- Classification: EfficientNet-B0
- Intel Geti에서 학습 후 → ONNX Export
- CUDA 기반 PC에서 실시간 추론
- 카메라 화이트밸런스·노출·초점 수동 설정으로 데이터 품질 개선
- Segmentation 결과의 픽셀 비율로 오염도 자동 계산

## 파일 구조
```
team2/
├─ iotdemo/
│   ├─ __init__.py
│   ├─ debounce.py
│   ├─ factory_controller.py
│   ├─ pins.py
│   ├─ pyduino.py
│   └─ pyft232.py
├─ MODEL_FILE
└─ run.py
```
