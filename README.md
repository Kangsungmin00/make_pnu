# make_pnu.ipynb

## 개요
`make_pnu.ipynb`는 공간데이터의 PNU(지번코드) 자동 생성, 데이터 표준화, 파일 저장 등 일련의 데이터 전처리 과정을 담고 있는 Jupyter Notebook입니다.

- **PNU**: 토지 및 공간 데이터의 고유 식별자로 사용되는 표준 지번코드
- **주요 목적**: SHP/CSV 등 공간데이터에서 PNU 생성 및 품질 통일 자동화

---

## 주요 기능
- SHP, CSV 등 다양한 공간 데이터 파일 불러오기
- PNU 컬럼 생성 및 보정
- 결측치, 공백, 포맷 등 데이터 표준화
- 처리 결과 저장(Shapefile, CSV 등 지원)

---

## 실행 환경

- **Python** 3.8 이상
- 주요 라이브러리:  
  - `geopandas`
  - `pandas`
  - `numpy` (필요시)
  - 기타: `os`, `warnings` 등

### 필수 패키지 설치
```
pip install geopandas pandas numpy
```

경고(warning) 메시지 숨기기
노트북 맨 앞(최상단 셀)에 아래 코드를 추가하면 모든 경고 메시지를 숨길 수 있습니다.

```
import warnings
warnings.filterwarnings('ignore')
```

# 사용 방법
1. Jupyter Notebook에서 make_pnu.ipynb를 엽니다.
2. 데이터 파일 경로와 주요 변수(컬럼명 등)를 본인 환경에 맞게 수정합니다.
3. 각 셀을 위에서 아래로 순서대로 실행합니다.
4. 결과 파일(CSV, SHP 등)을 지정 폴더에서 확인합니다.

#### 데이터 불러오기
```
df = gpd.read_file("input.shp")
```

#### PNU 컬럼 생성 (예시)
```
def make_pnu(row):
    # 데이터 컬럼 구조에 따라 수정
    return f"{row['CLSF_CD']}-{row['LDCG_CD']}-{row['SB_PNU']}"
df["PNU"] = df.apply(make_pnu, axis=1)
```

#### 결과 저장
```
df.to_file("output.shp")
```

## 참고 및 유의사항
1. 입력 파일의 컬럼명 및 구조에 따라 일부 코드는 직접 수정이 필요합니다.
2. 파일 경로, 포맷 등도 본인 환경에 맞게 조정하세요.
3. 파이썬 및 주요 패키지 버전이 맞지 않을 경우 오류가 발생할 수 있습니다.

