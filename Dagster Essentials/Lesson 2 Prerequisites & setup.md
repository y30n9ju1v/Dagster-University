## 필수 설치 사항

이 수업은 코딩 실습 위주로 진행됩니다. 수업을 따라가려면 개인 컴퓨터에 프로젝트를 로컬로 실행하거나, 모든 필수 사항이 설정된 Github Codespaces에서 코드를 작업할 수 있습니다.

**_다음 옵션 중 하나만 선택하여 설정하면 됩니다. 다른 옵션은 건너뛰세요._**

- [로컬 개발](https://dagster-university.vercel.app/installation/set-up-local)
    
- [Github Codespaces](https://dagster-university.vercel.app/installation/set-up-codespace)
    

# 로컬 설정

이 섹션은 로컬 머신에 Dagster를 설정하는 방법을 설명합니다. 이 과정을 Github Codespaces에서 진행하고 싶다면 [해당 가이드](https://dagster-university.vercel.app/dagster-essentials/lesson-2/2-set-up-codespace)를 따르세요.

- **Git 설치.** Git이 설치되어 있지 않다면 [Git 문서](https://github.com/git-guides/install-git)를 참조하세요.
    
- **Python 설치.** Dagster는 Python 3.9 - 3.12를 지원합니다(3.12 권장).
    
- **패키지 관리자 설치.** Python 패키지를 관리하기 위해 Dagster가 내부적으로 사용하는 [`uv`](https://www.google.com/search?q=%5Bhttps://dagster-university.vercel.app/installation/%5D\(https://dagster-university.vercel.app/installation/\)\(https:/docs.astral.sh/uv/\))를 권장합니다.
    

---

## Dagster University 프로젝트 복제

[Github 저장소를 복제](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository)하세요. 명령은 [ssh 또는 https](https://graphite.dev/guides/git-clone-ssh-vs-https) 중 어떤 방식으로 복제할지 선택하는지에 따라 달라집니다.

|옵션|명령어|
|---|---|
|ssh|`git clone git@github.com:dagster-io/project-dagster-university.git`|
|https|`git clone https://github.com/dagster-io/project-dagster-university.git`|

Dagster University 프로젝트를 복제한 후, 저장소 내의 특정 코스 디렉토리로 이동하세요. 모든 코스는 `dagster_university`폴더 안에 있습니다.

예를 들어, "Dagster Essentials"를 완료하는 경우 해당 디렉토리로 이동하세요.

Bash

```
cd dagster_university/dagster_essentials
```

## uv 및 dg 설치

이제 `dg`를 설치해야 합니다. 이것은 Dagster와 쉽게 상호 작용할 수 있도록 하는 명령줄 인터페이스입니다. 이 과정 전체에서 `dg`를 사용하여 프로젝트를 스캐폴딩하고 개발 프로세스를 간소화할 것입니다.

`dg`를 가장 잘 사용하려면 Python 패키지 관리자 [`uv`](https://www.google.com/search?q=%5Bhttps://docs.astral.sh/uv/)가](https://www.google.com/search?q=https://docs.astral.sh/uv/)%EA%B0%80) 필요합니다. `uv`는 `dg`를 전역적으로 설치하고 가상 환경을 더 쉽게 구축할 수 있도록 합니다.

아직 `uv`가 설치되어 있지 않다면 다음 명령으로 설치할 수 있습니다.

Bash

```
brew install uv
```

## 의존성 설치

[uv](https://docs.astral.sh/uv/)로 Python 의존성을 설치하려면 코스별 디렉토리에서 다음을 실행하세요.

Bash

```
uv sync
```

이렇게 하면 가상 환경이 생성되고 필요한 의존성이 설치됩니다. 새로 생성된 가상 환경에 들어가려면 다음을 실행하세요.

|운영체제|명령어|
|---|---|
|MacOS|`source .venv/bin/activate`|
|Windows|`.venv\Scripts\activate`|

---

**pip**

[pip](https://pypi.org/project/pip/)로 Python 의존성을 설치하려면 코스별 디렉토리에서 다음을 실행하세요.

Bash

```
python3 -m venv .venv
```

이렇게 하면 가상 환경이 생성됩니다. 새로 생성된 가상 환경에 들어가려면 다음을 실행하세요.

|운영체제|명령어|
|---|---|
|MacOS|`source .venv/bin/activate`|
|Windows|`.venv\Scripts\activate`|

필요한 의존성을 설치하려면 다음을 실행하세요.

Bash

```
pip install -e ".[dev]"
```

# 프로젝트 파일

Dagster Essentials 과정의 파일에 대해 잠시 이야기해 봅시다. `dagster_university/dagster_essentials` 디렉토리는 다음과 같아야 합니다.

Bash

```
dagster_university/dagster_essentials
.
├── dagster_cloud.yaml
├── data
├── Makefile
├── pyproject.toml
├── pytest.ini
├── README.md
├── src
│   ├── __init__.py
│   └── dagster_essentials
│       ├── __init__.py
│       ├── completed
│       └── defs
│           ├── __init__.py
│           ├── assets
│           │   └── constants.py
│           ├── jobs.py
│           ├── partitions.py
│           └── resources.py
├── tests
└── uv.lock
```

**지금은 몇 가지 파일만 다룰 예정입니다.** 하지만 나중 수업에서 추가 파일을 더 자세히 설명할 것입니다.

다음 표의 열은 다음과 같습니다.

- **파일/디렉토리 -** 파일/디렉토리의 이름
    
- **컨텍스트** - 프로젝트에 파일/디렉토리가 있는 이유. 파일/디렉토리가 다음임을 나타냅니다.
    
    - **Dagster -** 모든 Dagster 프로젝트에서 발견됩니다.
        
    - **Dagster U** - 특히 Dagster University에서 구축할 프로젝트를 위한 것입니다.
        
    - **Python** - 소프트웨어 엔지니어링 및 Python 모범 사례로 강력히 권장되지만, 기술적으로 Dagster에 의해 요구되지는 않습니다.
        
- **설명** - 파일/디렉토리가 포함하는 내용 또는 용도에 대한 설명
    

|파일/디렉토리|컨텍스트|설명|
|---|---|---|
|`README.md`|Python|Dagster 프로젝트에 대한 설명 및 시작 가이드입니다.|
|`dagster_essentials/`|Dagster U|이 과정 동안 작업할 파일이 포함되어 있습니다.|
|`src/dagster_essentials/completed/`|Dagster U|각 수업의 완성된 코드입니다.|
|`src/tests/`|Dagster U|완성된 코드에 대한 단위 테스트가 포함된 Python 모듈입니다.|
|`data/`|Dagster U|이 디렉토리(및 그 안의 디렉토리)는 이 과정 동안 만들 데이터 자산을 저장할 위치입니다. 프로덕션 설정에서는 Amazon S3 또는 데이터 웨어하우스일 수 있습니다.|
|`.env`|Python|미리 구성된 환경 변수가 포함된 텍스트 파일입니다. 외부 서비스 연결을 다루는 6과에서 이 파일에 대해 더 자세히 설명합니다.|
|`pyproject.toml`|Python|패키지 핵심 메타데이터를 정적이고 도구 독립적인 방식으로 지정하는 파일입니다. 이 파일에는 Dagster 정의가 최상위 수준에서 정의되고 검색 가능하도록 Python 모듈을 참조하는 `tool.dagster` 섹션이 포함되어 있습니다. 이를 통해 매개변수 없이 `dagster dev` 명령을 사용하여 Dagster 코드를 로드할 수 있습니다.|
|`pytest.ini`|Python|pytest.ini 파일은 pytest의 구성 파일로, 명령줄 옵션, 마커 및 플러그인 구성과 같은 테스트 설정을 정의할 수 있습니다.|
|`uv.lock`|Python|Python에서 `uv.lock`은 패키지 관리자 uv가 `poetry.lock` 또는 `requirements.txt`와 유사하게 종속성을 잠그는 데 사용하는 파일로, 재현 가능한 설치를 보장합니다.|

Dagster 프로젝트의 다른 파일에 대한 자세한 내용은 [Dagster 문서의 프로젝트 파일 참조](https://docs.dagster.io/guides/understanding-dagster-project-files)를 확인하세요.