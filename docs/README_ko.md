# 커밋 번역기
이 스크립트는 한국어 및 일본어로 작성된 커밋 메시지를 영어로 번역하고, 일반적인 커밋 규칙에 맞게 포맷합니다.

## 주요 기능
- **언어 지원**: 한국어와 일본어로 작성된 커밋 메시지를 영어로 번역합니다.
- **커밋 타입 자동 감지**: 입력된 메시지에 따라 커밋 타입(feat, fix, chore 등)을 자동으로 결정합니다.
- **확인 프롬프트**: 번역된 메시지를 확인한 후, 사용자가 커밋을 진행할지 여부를 선택할 수 있습니다.

## 사용 방법
### 1. Poetry 설치

- `Poetry`가 설치되어 있지 않은 경우, 아래 명령어를 통해 설치합니다.
   
    ```bash
    curl -sSL https://install.python-poetry.org | python3 -
    ```

- 셸 설정 파일에 PATH 추가 (예: ~/.bash_profile, ~/.zshrc)

    ```bash
    export PATH="$HOME/.poetry/bin:$PATH"
    ```

    Poetry에 대한 더 자세한 정보는 [공식 문서](https://python-poetry.org/docs/)를 참고해 주세요!

#### 1.1. Poetry를 사용하지 않는 경우

- `Poetry`를 설치하고 싶지 않은 경우, `openai`와 `python-dotenv` 패키지를 전역적으로 설치하여 사용할 수 있습니다. 아래 명령어를 사용하여 패키지를 설치합니다:

    ```bash
    pip install openai python-dotenv
    ```

### 2. 리포지토리 클론
    
- `GitHub`에서 이 리포지토리를 클론합니다.
   
    ```bash
    git clone https://github.com/BoYeonJang/commit-translator.git
    cd commit-translator
    ```

### 3. 가상환경 설정

- `Poetry`를 사용하여 필요한 패키지를 설치합니다.

    ```bash
    poetry install
    ```

### 4. OpenAI API 키 설정
    
- `.env.example` 파일의 이름을 `.env` 으로 변경하고, `your_openai_api_key_here` 부분을 자신의 OpenAI API 키로 변경합니다:

    ```bash
    OPENAI_API_KEY="your_openai_api_key_here"
    ```

### 5. 파일 다운로드 및 설정
#### 5.1. 파일 다운로드:

- `cmtl` 파일을 `curl`을 사용하여 다운로드합니다:

    ```bash
    curl -O https://gist.githubusercontent.com/BoYeonJang/a49de7f226f668a0cb1185fc808f42cf/raw/6638adae14589273e095cfab270db04c00793489/cmtl
    ```

#### 5.2. 파일 수정:

- `SCRIPT_DIR` 변수를 수정해야 합니다:

    ```bash
    vi cmtl
    ```

    ```bash
    3 # =============== Please revise this section ===============
    4 SCRIPT_DIR="/absolute/path/to/commit-translator"
    5 # ==========================================================
    ```

- 여기서 `/absolute/path/to/commit-translator`는 클론한 리포지토리의 절대 경로로 변경해야 합니다.

#### 5.3. 실행 권한 부여 및 시스템 경로로 이동:

- 실행 권한을 부여한 후, 파일을 `/usr/local/bin/` 디렉토리로 이동하여 전역에서 사용할 수 있도록 설정합니다:

    ```bash
    chmod +x cmtl && sudo mv cmtl /usr/local/bin/
    ```

#### 5.4 (옵션)

- 커밋을 실행할 것인지 묻는 메시지를 무시하려면:

    ```bash
    curl -O https://gist.githubusercontent.com/BoYeonJang/93a2d63ba8651a992f3e05e5475e91de/raw/a081a14d87981d9d3b46c667a27f5c565d628c9f/cmtl
    ```

    ```bash
    vi cmtl
    ```

    ```bash
    3 # =============== Please revise this section ===============
    4 SCRIPT_DIR="/absolute/path/to/commit-translator"
    5 # ==========================================================
    ```

    ```bash
    chmod +x cmtl && sudo mv cmtl /usr/local/bin/
    ```

<!-- ### 5. zsh 설정

- 셸 설정 파일을 열어 `cmtl` 함수를 추가합니다:

    ```bash
    function cmtl() {
        if [ "$#" -eq 0 ]; then
            echo "Usage: cmtl \"commit message\""
            return 1
        fi
        
        message="$*"
        
        commit_message=$(poetry run python /path/to/your/translate.py "$message")
        
        git commit -m "$commit_message"
    }
    ```

- `/path/to/your/translate.py` 부분은 클론한 리포지토리의 절대 경로로 변경하세요.

#### 5.1 (옵션)

- 커밋이 수행되기 전에 취소를 하고 싶다면:

    ```bash
    function cmtl() {
        if [ "$#" -eq 0 ]; then
            echo "Usage: cmtl \"commit message\""
            return 1
        fi
        
        message="$*"

        commit_message=$(poetry run python /path/to/your/translate.py "$message")
        
        echo "Translated commit message: $commit_message"
        echo "Do you want to proceed with the commit? (y/n)"
        
        read -r response
        if [[ "$response" == "y" ]]; then
            git commit -m "$commit_message"
            echo "commit successful!"
        else
            echo "commit canceled."
        fi
    }
    ```
    
- 변경사항 저장:
    ```bash
    source ~/.zshrc
    ``` -->

### 6. cmtl 명령어 사용

- 이제 `cmtl` 명령어를 사용하여 커밋 메시지를 번역하고 커밋할 수 있습니다. 예를 들어:

    ```bash
    cmtl "컴포넌트 추가"
    ```

- 일본어로 입력할 경우:

    ```bash
    cmtl "コンポーネント追加"
    ```

## 예제
아래는 스크립트를 사용하는 간단한 예제입니다:

한국어 메시지 입력:
```bash
cmtl "버그 수정"
```

출력:
```bash
fix: fix a bug
Do you want to proceed with the commit? (y/n)
```

일본어 메시지 입력:
```bash
cmtl "バグ修正"
```

출력:
```bash
fix: fix a bug
Do you want to proceed with the commit? (y/n)
```

## 기여 방법
기여를 원하신다면, 이 리포지토리를 포크한 후 수정 사항을 적용하여 풀 리퀘스트를 보내주시면 됩니다. 모든 기여는 환영합니다!

## 라이센스
이 프로젝트는 [MIT 라이센스](https://mit-license.org/)를 따릅니다.

## 문의
궁금한 사항이나 문제가 발생할 경우, 이슈를 통해 문의해 주세요.

# 파일 다운로드
curl -O https://gist.githubusercontent.com/BoYeonJang/a49de7f226f668a0cb1185fc808f42cf/raw/cc2a1f817d866ae7fdeed6af87ccbb8c5f6888dd/cmtl

# 실행 권한 부여
chmod +x cmtl

# 시스템 경로로 이동
sudo mv cmtl /usr/local/bin/