# Pandas 데이터 분석 필수 치트시트 (Cheat Sheet)

## 1. 라이브러리 임포트 및 데이터 불러오기/저장
가장 기초가 되는 파일 입출력 명령어입니다.

| 명령어 | 설명 | 예시 |
| :--- | :--- | :--- |
| `import pandas as pd` | Pandas 라이브러리 불러오기 | `import pandas as pd` |
| `pd.read_csv()` | CSV 파일 불러오기 | `df = pd.read_csv('data.csv')` |
| `pd.read_excel()` | 엑셀 파일 불러오기 | `df = pd.read_excel('data.xlsx')` |
| `df.to_csv()` | 데이터프레임을 CSV로 저장 | `df.to_csv('result.csv', index=False)` |

## 2. 데이터 확인 및 구조 파악 (Inspection)
데이터를 처음 받았을 때 가장 먼저 실행해야 하는 함수들입니다.

| 명령어 | 설명 | 예시 |
| :--- | :--- | :--- |
| `df.head(n)` | 상위 n개 행 출력 (기본 5개) | `df.head(3)` |
| `df.tail(n)` | 하위 n개 행 출력 | `df.tail()` |
| `df.info()` | 행/열 개수, 데이터 타입, 결측치 등 요약 정보 | `df.info()` |
| `df.shape` | 행과 열의 개수 (튜플 형태) | `rows, cols = df.shape` |
| `df.columns` | 컬럼 이름 확인 | `print(df.columns)` |
| `df.describe()` | 수치형 데이터의 기술 통계 (평균, 표준편차 등) | `df.describe()` |
| `df['col'].unique()` | 특정 컬럼의 고유값 확인 (중복 제거) | `df['species'].unique()` |
| `df['col'].value_counts()` | 특정 컬럼의 고유값 개수 카운트 | `df['island'].value_counts()` |

## 3. 데이터 선택 및 필터링 (Selection & Filtering)
원하는 데이터만 쏙쏙 뽑아내는 방법입니다.

| 구분 | 명령어 문법 | 설명 | 예시 |
| :--- | :--- | :--- | :--- |
| **컬럼 선택** | `df['col']` | 하나의 컬럼 선택 (Series 반환) | `df['species']` |
| **다중 컬럼** | `df[['col1', 'col2']]` | 여러 컬럼 선택 (DataFrame 반환) | `df[['species', 'sex']]` |
| **조건 필터링** | `df[조건]` | 조건에 맞는 행만 추출 | `df[df['age'] > 30]` |
| **다중 조건** | `&` (AND), `\|` (OR) | 여러 조건을 조합 (괄호 필수) | `df[(df['age'] > 20) & (df['sex'] == 'F')]` |
| **특정 값 포함** | `isin([값 리스트])` | 리스트 안에 있는 값인 경우 | `df[df['island'].isin(['Biscoe', 'Dream'])]` |
| **위치 기반** | `df.iloc[행, 열]` | **숫자 인덱스**로 위치 지정 | `df.iloc[0:5, 0:2]` (0~4행, 0~1열) |
| **라벨 기반** | `df.loc[행, 열]` | **이름(Label)**으로 위치 지정 | `df.loc[0:5, ['species', 'island']]` |

## 4. 데이터 전처리 및 결측치 처리 (Cleaning)
데이터 분석의 80%를 차지하는 전처리 과정입니다.

| 명령어 | 설명 | 예시 |
| :--- | :--- | :--- |
| `df.isnull().sum()` | 컬럼별 결측치(NaN) 개수 확인 | `df.isnull().sum()` |
| `df.dropna()` | 결측치가 포함된 행 제거 | `df.dropna()` / `df.dropna(axis=1)` (열 제거) |
| `df.fillna(값)` | 결측치를 특정 값으로 채움 | `df.fillna(0)` / `df.fillna(df.mean())` |
| `df.duplicated().sum()` | 중복된 행 개수 확인 | `df.duplicated().sum()` |
| `df.drop_duplicates()` | 중복된 행 제거 | `df.drop_duplicates()` |
| `df.astype(타입)` | 데이터 타입 변환 | `df['id'] = df['id'].astype(str)` |
| `df.drop(컬럼, axis=1)` | 불필요한 컬럼 삭제 | `df.drop(['col1', 'col2'], axis=1)` |

## 5. 데이터 가공 및 변형 (Manipulation)
데이터를 입맛에 맞게 수정하는 명령어입니다.

| 명령어 | 설명 | 예시 |
| :--- | :--- | :--- |
| `df.rename(columns={})` | 컬럼 이름 변경 | `df.rename(columns={'old': 'new'})` |
| `df.sort_values(by='col')` | 값 정렬 (오름차순) | `df.sort_values(by='age', ascending=False)` |
| `df.apply(함수)` | 함수 적용 (주로 복잡한 연산 시) | `df['col'].apply(lambda x: x*2)` |
| `df['col'].map(딕셔너리)` | 값을 매핑하여 변환 | `df['sex'].map({'Male': 0, 'Female': 1})` |
| `df['col'].str` | 문자열 처리 접근자 | `df['name'].str.upper()` / `df['name'].str.contains('Kim')` |

## 6. 통계 및 그룹화 (Aggregation)
데이터의 인사이트를 뽑아내는 핵심 단계입니다.

| 명령어 | 설명 | 예시 |
| :--- | :--- | :--- |
| `df.groupby('col')` | 특정 컬럼 기준으로 그룹화 | `df.groupby('species')['mass'].mean()` |
| `df.pivot_table()` | 엑셀의 피벗 테이블과 동일 | `df.pivot_table(index='A', columns='B', values='C')` |
| `df.corr()` | 컬럼 간 상관계수 확인 | `df.corr()` |
| `agg(['mean', 'sum'])` | 여러 통계 함수 동시 적용 | `df.groupby('species')['mass'].agg(['mean', 'max'])` |

---

### 💡 Tip: `inplace=True` vs 재할당
Pandas의 많은 함수들은 원본 데이터를 바로 수정하지 않고, **수정된 복사본을 반환**합니다. 원본을 변경하려면 다음 두 가지 중 하나를 선택해야 합니다.

1.  **변수에 다시 저장하기 (추천):**
    `df = df.dropna()`
2.  **`inplace=True` 옵션 사용하기:**
    `df.dropna(inplace=True)`