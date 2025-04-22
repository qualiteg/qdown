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
file_path = qdown.download("https://drive.qualiteg.com/file/abCD-ef12-ghIJklMNopQR", 
                         output_path="/home/user/downloads/my_file.txt")

# 出力フルパスを指定（位置引数）
file_path = qdown.download("https://drive.qualiteg.com/file/abCD-ef12-ghIJklMNopQR", 
                         "/home/user/downloads/my_file.txt")

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