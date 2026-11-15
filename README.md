# KISTI 선박 항적 데이터 AI 분석

KISTI 대회 제공 선박 항적에서 계산한 특징을 사용해 조업 유형을 분류하고 이상 항적을 점수화합니다. 최종 패키지 버전은 `kisti-final-20261101-v1`입니다.

- **과제 A · 조업 유형 분류** — LightGBM 모델로 시간대별 클래스 확률을 구하고 선박별 유형을 예측합니다. 전체 홀드아웃 재평가를 선택할 수 있습니다.
- **과제 B · 이상 항적 점수화** — 제공된 Test B 성분으로 확정 점수를 재현합니다. 새 입력 예제에는 별도로 재학습한 모델을 사용합니다.

## 파일

| 파일 | 용도 |
| --- | --- |
| [final_fishing_model.ipynb](%EA%B9%80%ED%98%84%EC%9E%AC_%EC%B5%9C%EC%A2%85/final_fishing_model.ipynb) | Colab 실행 노트북 |
| [final_model_assets.zip](%EA%B9%80%ED%98%84%EC%9E%AC_%EC%B5%9C%EC%A2%85/final_model_assets.zip) | 모델, 파생 특징, 평가 입력 및 실행 코드. 약 278 MiB이며 Git LFS로 관리합니다. |
| [MODEL_DESIGN_AND_USAGE.md](%EA%B9%80%ED%98%84%EC%9E%AC_%EC%B5%9C%EC%A2%85/MODEL_DESIGN_AND_USAGE.md) | 모델 설계, 데이터 출처, 입력 형식 및 검증 기록 |

## Colab 실행

1. 노트북을 Colab에서 엽니다. GitHub에서 `final_model_assets.zip`을 다운로드해 Colab 파일 패널에 올리거나 Google Drive에 둡니다. 로컬에서 저장소를 내려받았다면 Git LFS 설치 후 `git lfs pull`로 ZIP을 받을 수 있습니다.
2. 설정 셀의 `BASE_DIR`을 ZIP이 있는 폴더로 지정합니다. Drive를 사용한다면 먼저 마운트합니다. ZIP은 노트북이 직접 풉니다.
3. 위에서부터 셀을 실행합니다. Python 3.11 이상과 CPU 런타임을 사용하며, 첫 실행에서 패키지를 설치할 수 있습니다. 기본값에서 전체 홀드아웃 재평가와 새 B 입력 예제도 실행됩니다. 기본 Test A·B 결과만 재현하려면 `RUN_HOLDOUT_EVALUATION`과 `RUN_NEW_B_EXAMPLE`을 `False`로 설정합니다.
4. `BASE_DIR` 아래 `outputs/final_run_*/`에서 예측, 평가 지표, 실행 기록을 확인합니다.

## 입력과 결과 해석

노트북은 사전에 계산된 특징부터 실행합니다. 새 원시 WKT 항적을 사용하려면 상세 문서의 특징 정의에 맞는 전처리가 필요합니다. 과제 B의 이상점수는 항적을 검토하는 지표이며, 사고 라벨이 없어 사고 탐지 성능과 공식 점수는 산출하지 않습니다.
