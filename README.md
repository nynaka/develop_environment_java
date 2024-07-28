このリポジトリ
===

Java 開発環境構築メモです。

## doc のビルド方法

- venv のインストール

    ```bash
    sudo apt install python3-venv
    ```

- venv 環境作成と有効化

    ```bash
    python3 -m venv venv
    source ./venv/bin/activate
    ```

- ドキュメントのビルドツールのインストール

    ```bash
    pip install --break-system-packages \
        sphinx sphinx_rtd_theme \
        sphinxcontrib-actdiag \
        sphinxcontrib-blockdiag \
        sphinxcontrib-nwdiag \
        sphinxcontrib-seqdiag \
        myst_parser sphinx_markdown_tables
    ```

- 日本語フォントのインストール

    ```bash
    sudo apt install -y \
        fonts-ipafont fonts-ipaexfont
    ```

- source/conf.py の設定

    <details>
    <summary>主な変更差分</summary>
    
    ```diff
    --- /tmp/conf.py        2024-07-28 11:14:42.235214472 +0900
    +++ conf.py     2024-07-28 11:15:47.945348657 +0900
    @@ -16,7 +16,21 @@
     # -- General configuration ---------------------------------------------------
     # https://www.sphinx-doc.org/en/master/usage/configuration.html#general-configuration
    
    -extensions = []
    +extensions = [
    +    'myst_parser',         # MyST (Markedly Structured Text) パーサーを有効化
    +    'sphinx_markdown_tables',
    +    'sphinxcontrib.blockdiag',
    +    'sphinxcontrib.seqdiag',
    +    'sphinxcontrib.actdiag',
    +    'sphinxcontrib.nwdiag',
    +    'sphinxcontrib.rackdiag',
    +    'sphinxcontrib.packetdiag',
    +]
    +
    +source_suffix = {
    +    '.rst': 'restructuredtext',
    +    '.md': 'markdown',  # Markdownの拡張子を設定
    +}
    
     templates_path = ['_templates']
     exclude_patterns = []
    @@ -26,5 +40,5 @@
     # -- Options for HTML output -------------------------------------------------
     # https://www.sphinx-doc.org/en/master/usage/configuration.html#options-for-html-output
    
    -html_theme = 'alabaster'
    +html_theme = 'sphinx_rtd_theme'
     html_static_path = ['_static']
    ```
    <details>

- ドキュメントのビルド

    ```bash
    make html
    ```

    カレントディレクトリ配下に `build` ディレクトリが作成されます。


## sample コードのビルドに必要なパッケージ

- Ubuntu Server 24.04

    ````bash
    sudo apt install -y \
        openjdk-21-jdk \
        openjdk-21-jdk-headless \
        maven
    ```

- 環境変数 `JAVA_HOME` の設定

    ```bash
    echo "export JAVA_HOME=`echo $(dirname $(readlink $(readlink $(which java)))) | sed -e 's/\/bin$//g' | sed -e 's/\/jre$//g'`" \
        >> $HOME/.bashrc
    source $HOME/.bashrc
    ```
