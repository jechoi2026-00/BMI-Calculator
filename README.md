# BMI Calculator Web Application

체중과 신장을 입력하면 BMI를 계산하고, 계산 결과를 데이터베이스에 저장한 뒤 결과 페이지와 히스토리 페이지에서 확인할 수 있는 Flask 기반 웹 애플리케이션입니다.

---

## 프로젝트 개요

이 프로젝트는 사용자가 입력한 체중과 신장을 바탕으로 BMI를 계산하고, BMI 수치에 따라 건강 상태를 분류하는 간단한 웹 애플리케이션입니다.

계산된 결과는 MariaDB 또는 MySQL 데이터베이스에 저장되며, 사용자는 이전 계산 기록을 히스토리 페이지에서 확인하거나 삭제할 수 있습니다.

---

## 주요 기능

- 체중과 신장 입력을 통한 BMI 계산
- BMI 수치에 따른 건강 상태 분류
- 계산 결과 데이터베이스 저장
- 과거 BMI 계산 기록 조회
- BMI 기록 삭제
- Flask 기반 웹 페이지 구성
- MariaDB/MySQL 연동
- 환경변수를 이용한 데이터베이스 설정
- Cloudtype 배포 설정 지원

---

## 기술 스택

<p align="left">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white" alt="Flask"/>
  <img src="https://img.shields.io/badge/Jinja-B41717?style=for-the-badge&logo=jinja&logoColor=white" alt="Jinja2"/>
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white" alt="HTML5"/>
  <img src="https://img.shields.io/badge/CSS3-663399?style=for-the-badge&logo=css&logoColor=white" alt="CSS3"/>
  <img src="https://img.shields.io/badge/MariaDB-003545?style=for-the-badge&logo=mariadb&logoColor=white" alt="MariaDB"/>
  <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL"/>
  <img src="https://img.shields.io/badge/PyMySQL-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="PyMySQL"/>
  <img src="https://img.shields.io/badge/Gunicorn-499848?style=for-the-badge&logo=gunicorn&logoColor=white" alt="Gunicorn"/>
  <img src="https://img.shields.io/badge/Cloudtype-000000?style=for-the-badge&logo=cloudflare&logoColor=white" alt="Cloudtype"/>
</p>

| 구분 | 사용 기술 |
|---|---|
| Backend | Python, Flask |
| Database | MariaDB / MySQL |
| DB Connector | PyMySQL |
| Template | Jinja2, HTML |
| Styling | CSS |
| Deployment | Cloudtype, Gunicorn |

---

## 프로젝트 구조

```text
BMI-Calculator/
├── app.py                    # Flask 애플리케이션 메인 파일
├── bmi.py                    # BMI 계산 로직 클래스
├── db.py                     # 데이터베이스 연결 및 관리 클래스
├── requirements.txt          # Python 패키지 목록
├── flaskexample.yaml         # Cloudtype 배포 설정 파일
├── templates/
│   ├── index.html            # 체중, 신장 입력 페이지
│   ├── result.html           # BMI 계산 결과 페이지
│   └── history.html          # BMI 계산 기록 페이지
├── static/
│   └── style.css             # 웹 페이지 스타일 파일
└── .github/
    └── workflows/            # GitHub Actions 관련 설정
```

---

## 파일별 설명

### `app.py`

Flask 웹 애플리케이션의 메인 파일입니다.

주요 역할은 다음과 같습니다.

- `/` : BMI 입력 페이지 렌더링
- `/calculate` : BMI 계산 및 결과 저장
- `/history` : 과거 계산 기록 조회
- `/delete/<id>` : 특정 BMI 기록 삭제
- 데이터베이스 연결 설정
- 예외 처리 및 flash 메시지 처리

데이터베이스 연결 정보는 코드에 직접 고정하지 않고 환경변수에서 읽어오도록 구성되어 있습니다.

---

### `bmi.py`

BMI 계산을 담당하는 클래스 파일입니다.

주요 기능은 다음과 같습니다.

- 신장 cm 값을 m 단위로 변환
- BMI 계산
- BMI 결과 반올림
- BMI 기준에 따른 상태 분류

BMI 계산 공식은 다음과 같습니다.

```text
BMI = 체중(kg) / 신장(m)^2
```

---

### `db.py`

MariaDB 또는 MySQL 데이터베이스와 연결하고 BMI 결과를 관리하는 파일입니다.

주요 기능은 다음과 같습니다.

- 데이터베이스 연결
- 데이터베이스가 없을 경우 자동 생성
- `bmi_results` 테이블 생성
- BMI 결과 저장
- 전체 BMI 기록 조회
- 특정 기록 삭제
- 데이터베이스 연결 종료

---

## BMI 분류 기준

| 분류 | BMI 범위 |
|---|---|
| 저체중 | BMI < 18.5 |
| 정상체중 | 18.5 ≤ BMI < 25 |
| 과체중 | 25 ≤ BMI < 30 |
| 비만 | BMI ≥ 30 |

---

## 설치 및 실행 방법

### 1. 저장소 클론

```bash
git clone https://github.com/jechoi2026-00/BMI-Calculator.git
cd BMI-Calculator
```

---

### 2. 가상환경 생성 및 활성화

Windows PowerShell 기준:

```bash
python -m venv .venv
.venv\Scripts\activate
```

macOS 또는 Linux 기준:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

---

### 3. 패키지 설치

```bash
pip install -r requirements.txt
```

Cloudtype 또는 Gunicorn으로 배포할 경우 `gunicorn`도 필요할 수 있습니다.

```bash
pip install gunicorn
```

---

### 4. MariaDB 또는 MySQL 데이터베이스 준비

로컬 환경에서 MariaDB/MySQL을 사용하는 경우 다음과 같이 데이터베이스를 생성할 수 있습니다.

```sql
CREATE DATABASE bmi_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

기본 설정 예시는 다음과 같습니다.

| 항목 | 기본값 |
|---|---|
| Host | localhost |
| Port | 3306 |
| User | root |
| Password | 123 |
| Database | bmi_db |

---

### 5. 환경변수 설정

이 프로젝트는 데이터베이스 접속 정보를 환경변수로 관리할 수 있습니다.

사용 가능한 환경변수는 다음과 같습니다.

| 목적 | 기본 환경변수 | 대체 환경변수 |
|---|---|---|
| DB Host | `DB_HOST` | `MARIADB_HOST`, `MYSQL_HOST` |
| DB User | `DB_USER` | `MARIADB_USER`, `MYSQL_USER` |
| DB Password | `DB_PASSWORD` | `MARIADB_PASSWORD`, `MYSQL_PASSWORD` |
| DB Name | `DB_NAME` | `MARIADB_DATABASE`, `MYSQL_DATABASE` |
| DB Port | `DB_PORT` | `MARIADB_PORT`, `MYSQL_PORT` |

Windows PowerShell 예시:

```bash
$env:DB_HOST="localhost"
$env:DB_USER="root"
$env:DB_PASSWORD="123"
$env:DB_NAME="bmi_db"
$env:DB_PORT="3306"
```

macOS/Linux 예시:

```bash
export DB_HOST=localhost
export DB_USER=root
export DB_PASSWORD=123
export DB_NAME=bmi_db
export DB_PORT=3306
```

---

### 6. 애플리케이션 실행

```bash
python app.py
```

실행 후 브라우저에서 다음 주소로 접속합니다.

```text
http://localhost:5000
```

---

## 사용 방법

1. 메인 페이지에서 체중과 신장을 입력합니다.
2. `BMI 계산` 버튼을 클릭합니다.
3. 계산된 BMI 값과 건강 상태를 확인합니다.
4. `히스토리` 페이지에서 이전 계산 기록을 확인할 수 있습니다.
5. 필요 없는 기록은 삭제할 수 있습니다.

---

## Cloudtype 배포

이 프로젝트는 `flaskexample.yaml` 파일을 통해 Cloudtype 배포 설정을 포함하고 있습니다.

Cloudtype 배포 시 주요 설정은 다음과 같습니다.

```yaml
name: flaskexample
app: python@3.10
ports: 5000
start: gunicorn -b 0.0.0.0:5000 app:app
```

배포 환경에서는 데이터베이스 연결 정보를 Cloudtype 환경변수로 등록해야 합니다.

예시:

```text
DB_HOST=mariadb
DB_USER=root
DB_PASSWORD=123
DB_NAME=bmi_db
DB_PORT=3306
```

또는 Cloudtype에서 자동 주입하는 MariaDB 환경변수명을 사용할 수도 있습니다.

```text
MARIADB_HOST
MARIADB_USER
MARIADB_PASSWORD
MARIADB_DATABASE
MARIADB_PORT
```

---

## requirements.txt

현재 프로젝트에서 사용하는 주요 패키지는 다음과 같습니다.

```text
Flask==2.3.3
Werkzeug==2.3.7
pymysql==1.1.0
```

배포 환경에서 Gunicorn을 사용하는 경우 다음 항목을 추가하는 것을 권장합니다.

```text
gunicorn
```

---

## 데이터베이스 테이블 구조

BMI 결과는 `bmi_results` 테이블에 저장됩니다.

| 컬럼명 | 타입 | 설명 |
|---|---|---|
| id | INT | 기본키, 자동 증가 |
| weight | FLOAT | 체중 kg |
| height | FLOAT | 신장 cm |
| bmi | FLOAT | 계산된 BMI |
| status | VARCHAR(50) | BMI 분류 결과 |
| created_at | TIMESTAMP | 기록 생성 시간 |

---

## 주의사항

- MariaDB 또는 MySQL 서버가 실행 중이어야 합니다.
- 데이터베이스 접속 정보가 올바르게 설정되어 있어야 합니다.
- Cloudtype 배포 시 환경변수를 반드시 확인해야 합니다.
- `gunicorn`으로 실행할 경우 `requirements.txt`에 `gunicorn`을 추가하는 것이 좋습니다.
- `.venv`, `__pycache__`, 로컬 DB 파일 등은 일반적으로 Git에 올리지 않는 것이 좋습니다.

---

## 향후 개선 가능 사항

- 사용자별 BMI 기록 관리 기능 추가
- BMI 변화 추이 그래프 추가
- 입력값 검증 강화
- 로그인 기능 추가
- Docker 배포 환경 구성
- GitHub Actions를 이용한 자동 배포 구성
- SQLite 개발 환경과 MariaDB 배포 환경 분리

---

## 라이선스

이 프로젝트는 학습 및 개인 프로젝트 목적으로 자유롭게 사용할 수 있습니다.
