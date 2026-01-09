
# Intel Geti + AI QC Conveyor

<img width="849" height="454" alt="image" src="https://github.com/user-attachments/assets/c85cd102-639c-454f-b1aa-e15400428c58" />


공장 생산라인에서 병뚜껑의 QC 스티커 유무와 오염도 비율을 AI 모델이 자동 분석하고, 분석 결과에 따라 아두이노 기반 포토센서와 액추에이터가 실시간으로 제품을 자동 분류하는 **End-To-End 스마트 팩토리 시스템**입니다.
<br> 또한, 버튼 하나로 동일 생산라인에서 분류 기준을 전환할 수 있도록 설계하여, 실제 산업 현장에 적용 가능한 확장형 스마트 팩토리 구조를 구현했습니다.

## 프로젝트 개요
- **목표**
  - 병뚜껑 QC 스티커 유무 판별
  - 오염 영역 Segmentation 기반 정량적 오염률 계산
  - AI 판단 결과에 따른 실시간 물리 분류 자동화

- **핵심 특징**
  - Detection + Segmentation + Classification **멀티 모델 파이프라인**
  - Intel Geti 기반 **산업용 AI 모델 관리**
  - Arduino + 액추에이터 연동 **완전 자동 분류**
  - Pink / Purple 모델 **버튼 전환 방식 운영**
  
## 개발 기간
* 25.09.24 - 25.10.22

## 개발 환경
<img width="877" height="419" alt="image" src="https://github.com/user-attachments/assets/f8453c52-d4d0-4e05-a156-402d462bb435" />

| Category | Stack |
|--------|------|
| AI Platform | Intel Geti |
| Language | Python 3.12.3 |
| Embedded | Arduino Mega |
| Database | MariaDB 10 |
| GUI | Tkinter |
| Model Export | ONNX |
| Inference | CUDA 기반 PC |

---

## 주요 기능

<img width="1364" height="778" alt="image" src="https://github.com/user-attachments/assets/6b540a2e-67d9-4927-a313-70f6181f2dc2" />
<img width="1396" height="684" alt="image" src="https://github.com/user-attachments/assets/7226819d-1d75-4470-99a0-d99a6cc50ed3" />

### 1. Segmentation 기반 정량적 오염률 계산
- Segmentation 모델을 활용한 **오염 영역 픽셀 단위 분할**
- 병뚜껑 전체 대비 오염 비율 계산을 통한 정량적 품질 평가
- Segmentation 결과를 활용하여 오염률을 계산

```text
오염률 (%) = (stain_px / cap_px) × 100
```

### 2. AI 기반 병뚜껑 자동 QC 판별
- Intel Geti 기반 AI 모델을 활용한 **실시간 병뚜껑 품질 검사**
- Pink / Purple 병뚜껑 색상 자동 인식
- QC 스티커 유무 정확 판별

### 3️. 색상별 QC 기준 분리 모델 운영

#### 🔴 Model 1 : Pink 병뚜껑 기준
- QC 스티커 유무 및 오염 여부 판별

- **완전불량**
  - QC 스티커 없음
  - 오염률 30% 초과
  - Purple 병뚜껑 감지

- **부분불량**
  - QC 스티커 존재 + 오염률 0% 초과 ~ 30% 이하

- **정상**
  - QC 스티커 존재 + 오염률 0%

---

#### 🟣 Model 2 : Purple 병뚜껑 기준
- QC 스티커 유무 및 오염 여부 판별

- **완전불량**
  - QC 스티커 없음
  - 오염률 30% 초과
  - Pink 병뚜껑 감지

- **부분불량**
  - QC 스티커 존재 + 오염률 0% 초과 ~ 30% 이하

- **정상**
  - QC 스티커 존재 + 오염률 0%


#### 관리자 모드
- 수동 컨베이어 제어
- 수동 엑츄에이터 조작
  
---

#### AI 모델 개발 과정
<img width="1076" height="557" alt="image" src="https://github.com/user-attachments/assets/5eb74f79-46a2-471a-bfe4-f8d340146d8a" />

   | Stage | Model / Tool | Description |
   |------|-------------|-------------|
   | Detection | **YOLOX-Tiny** | 제품 위치 및 QC 스티커 영역 검출 |
   | Segmentation | **SegNext-S** | 오염 영역 픽셀 단위 분할 |
   | Classification | **EfficientNet-B0** | 정상 / 부분 불량 / 완전 불량 분류 |
   | Training | **Intel Geti** | 모델 학습 및 성능 관리 |
   | Export | **ONNX** | OpenVINO·CUDA 환경 추론용 모델 변환 |
   | Inference | **CUDA 기반 PC** | 실시간 추론 파이프라인 구성 |
   | Data Quality | Camera Tuning | 화이트밸런스·노출·초점 수동 설정 |
