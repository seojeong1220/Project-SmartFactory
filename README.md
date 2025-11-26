<img width="1260" height="891" alt="Image" src="https://github.com/user-attachments/assets/600a07b7-64cd-4822-b122-ef01c0ea5cd6" />

# Intel Geti + AI QC Conveyor
인텔 Geti + 인공지능 QC 컨베이어


## 프로젝트 소개
인건비 절감을 위한 생산 공장 컨베이어 자동화 장치 입니다.
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
