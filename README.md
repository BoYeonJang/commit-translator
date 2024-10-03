# Commit Translator

- [ko](docs/README_ko.md)
- [jp](docs/README_jp.md)

This script translates commit messages written in Korean and Japanese into English and formats them according to common commit rules.

## Features
- **Language Support**: Translates commit messages written in Korean and Japanese into English.
- **Automatic Commit Type Detection**: Automatically determines the commit type (feat, fix, chore, etc.) based on the input message.
- **Confirmation Prompt**: After translating the message, users can choose whether to proceed with the commit.

## Usage
### 1. Install Poetry

- If Poetry is not installed, install it using the command below:

    ```bash
    curl -sSL https://install.python-poetry.org | python3 -
    ```

- Add PATH to your shell configuration file (e.g., ~/.bash_profile, ~/.zshrc)

    ```bash
    export PATH="$HOME/.poetry/bin:$PATH"
    ```

    For more details about Poetry, refer to the official documentation!

#### 1.1. If you don’t want to use Poetry

- If you prefer not to install Poetry, you can install the openai and python-dotenv packages globally. Use the command below to install the packages:

    ```bash
    pip install openai python-dotenv
    ```

### 2. Clone the Repository

- Clone this repository from GitHub.

    ```bash
    git clone https://github.com/BoYeonJang/commit-translator.git
    cd commit-translator
    ```

### 3. Set Up Virtual Environment

- Install the required packages using Poetry.

    ```bash
    poetry install
    ```

### 4. Set Up OpenAI API Key

- Create a .env file in the project root directory and add your API key:

    ```bash
    echo 'OPENAI_API_KEY="your_openai_api_key_here"' > .env
    ```

### 5. Set Up zsh

- Open your shell configuration file and add the cmtl function:

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

- Replace /path/to/your/translate.py with the actual path to the script.

#### 5.1 (Optional)

- If you want to cancel before the commit is made:

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

- Save the changes:
    ```bash
    source ~/.zshrc
    ```

### 6. Using the cmtl Command

- You can now use the cmtl command to translate commit messages and commit. For example:

    ```bash
    cmtl "Add component"
    ```

- If you enter in Japanese:

    ```bash
    cmtl "コンポーネント追加"
    ```

## Installation
To set up the script for global use, copy the cmtl command to /usr/local/bin using the command below.

```bash
sudo cp translate.py /usr/local/bin/cmtl
```
You can now use the cmtl command directly in the terminal.

#### (Optional)
If you do not want to install:

```bash
python translate.py "commit message"
```

## Example
Here’s a simple example of using the script:

Input a Korean message:
```bash
cmtl "버그 수정"
```

Output:
```bash
fix: fix a bug
Do you want to proceed with the commit? (y/n)
```

Input a Japanese message:
```bash
cmtl "バグ修正"
```
Output:
```bash
fix: fix a bug
Do you want to proceed with the commit? (y/n)
```

## Contributing
If you would like to contribute, please fork this repository, apply your modifications, and submit a pull request. All contributions are welcome!

## License
This project follows the [MIT License](https://mit-license.org/).

## Contact
If you have any questions or encounter issues, please reach out via issues.