# QDown 

QDown は Qualiteg Drive ファイルをダウンロードするためのシンプルなクライアントです。

## インストール

```bash
pip install qdown
```

## 使用方法

### コマンドライン

```bash
# 基本的な使い方
qdown ファイルID

# 出力ファイル名を指定
qdown ファイルID -O 出力ファイル名.txt

# 出力ディレクトリを指定
qdown ファイルID -o ./ダウンロード先/

# サーバーURLを指定
qdown ファイルID -s https://カスタムサーバー.com

# 進捗表示を非表示
qdown ファイルID --quiet
```

#### 新機能（v1.1以降）

大容量ファイル対応とパフォーマンス改善のための新オプション：

```bash
# 存在確認をスキップして最速ダウンロード（大容量ファイル推奨）
qdown ファイルID -O output.zip --skip-check

# 従来のHEADリクエストを使用（互換性のため）
qdown ファイルID --use-head

# 組み合わせ例：静かに最速ダウンロード
qdown ファイルID -q --skip-check -O large_file.zip
```

**新オプション説明：**
- `--skip-check`: ファイル存在確認をスキップ（最速ダウンロード）
- `--use-head`: HEADリクエストを使用（デフォルトは無効）

**改善点：**
- デフォルトでHEADリクエストをスキップ（大容量ファイルのタイムアウト問題を解決）
- `/file/{id}` エンドポイントでの存在確認（より確実）

### Python API

```python
import qdown

# ファイル共有リンクからダウンロード
file_path = qdown.download("https://drive.qualiteg.com/file/abCD-ef12-ghIJklMNopQR")

# ダウンロード直リンクからダウンロード
file_path = qdown.download("https://drive.qualiteg.com/download/zyXW-vu98-tsRQponMLkJ")

# ファイルIDを直接指定してダウンロード
file_path = qdown.download("abCD-ef12-ghIJklMNopQR")

# 出力ファイル名を指定（キーワード引数）
file_path = qdown.download("https://drive.qualiteg.com/file/abCD-ef12-ghIJklMNopQR", output_path="my_file.txt")

# 出力ファイル名を指定（位置引数）
file_path = qdown.download("https://drive.qualiteg.com/file/abCD-ef12-ghIJklMNopQR", "my_file.txt")

# 出力フルパスを指定（キーワード引数）
file_path = qdown.download("https://drive.qualiteg.com/file/abCD-ef12-ghIJklMNopQR", output_path="/home/user/downloads/my_file.txt")

# 出力フルパスを指定（位置引数）
file_path = qdown.download("https://drive.qualiteg.com/file/abCD-ef12-ghIJklMNopQR", "/home/user/downloads/my_file.txt")

# 進捗表示を非表示
file_path = qdown.download("https://drive.qualiteg.com/file/abCD-ef12-ghIJklMNopQR", quiet=True)

# 全オプションを指定
file_path = qdown.download(
    "https://drive.qualiteg.com/file/abCD-ef12-ghIJklMNopQR",
    output_path="my_file.txt",
    output_dir="./downloads",
    server_url="https://drive.qualiteg.com",
    quiet=False
)
```

#### 新機能（v1.1以降）- Python API

```python
import qdown

# 存在確認をスキップして高速ダウンロード（大容量ファイル推奨）
file_path = qdown.download(
    "abCD-ef12-ghIJklMNopQR",
    output_path="large_file.zip",
    skip_exists_check=True  # 新オプション
)

# HEADリクエストを使用（従来動作）
file_path = qdown.download(
    "abCD-ef12-ghIJklMNopQR",
    skip_head=False  # デフォルトはTrue（HEADスキップ）
)

# 最速設定：すべてのチェックをスキップ
file_path = qdown.download(
    "abCD-ef12-ghIJklMNopQR",
    output_path="huge_file.zip",
    skip_exists_check=True,
    skip_head=True,  # デフォルトで有効
    quiet=True
)
```

**新パラメータ説明：**
- `skip_exists_check`: 存在確認をスキップ（デフォルト: False）
- `skip_head`: HEADリクエストをスキップ（デフォルト: True）