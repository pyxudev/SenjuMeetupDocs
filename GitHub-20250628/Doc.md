# GitHub ハンズオン
PowerPoint: https://drive.google.com/drive/folders/1TiKKIUH7VcA-JaPUP3rcP1R9GLzjDidq?usp=sharing

## ゴール
- GitHub の基本操作を理解する
- 実際にリポジトリを操作してみる

## GitHub とは
ソースコードやドキュメントを管理・共有するためのWebサービス
- Git と GitHub の違い
  - Git：バージョン管理システム、Github：Git をベースにして、複数の開発者が協力してプロジェクトを進めることができるプラットフォーム
- GitHub の主な用途とメリット
  - チーム開発、履歴管理、レビュー、CI/CDなど、現代の開発に不可欠な機能が揃っている

## Git の基本概念
- リポジトリ（Repository）
  - プロジェクトのファイルとその履歴を保存する場所。
- コミット（Commit）
  - ファイルの変更を記録する単位。スナップショットのようなもの。
- ブランチ（Branch）
  - 作業の分岐。新機能や修正を本線（main）から切り離して行う。
- マージ（Merge）
  - 他ブランチでの作業を一つのブランチ（main）に統合する操作。

## GitHub の基本操作
- アカウント作成
  - GitHub 公式サイトで無料登録。
- リポジトリの作成
  - 新規プロジェクトを作成し、README やライセンスを追加。
- README の作成と編集
  - プロジェクトの概要や使い方を記載する Markdown ファイル。
- ファイルのアップロード
  - Web UI から直接ファイルを追加・編集可能。

## Git のローカル操作と GitHub との連携 CLI を使ってみよう
前提：ssh-agent が動いていることを確認し、GitHub に登録し、[git](https://git-scm.com/downloads) をインストールする
- Windows: https://git-scm.com/downloads
- Linux： 
```
sudo apt install git
sudo yum install git
sudo dnf install git
```
いずれかを使用

- SSH とは
  - 22 番ポートを使った暗号化された通信
  - リモートマシンに安全にログイン、コマンドを実行、ファイルを転送（SCP や SFTP）
  - 公開鍵暗号方式とも呼ばれる
  - サーバー上に公開鍵を配置し、ローカルに秘密鍵を置く

1. SSH キーの生成

Windows: C:\Users\your_usrname\.ssh<br>
Linux: home/.ssh<br>
にて
```
$ ssh-keygen -t ed25519 -C "your_email@example.com"
```

2. config ファイルの作成

上記 1. の .ssh ディレクトリにて config ファイルを作成し以下を入力
```
Host github
  HostName github.com
  IdentityFile ~/.ssh/your_keyname
  User git
```

3.SSH キーの追加

[ settings ] → [ SSH and GCP keys ] → [ New SSH Key ] をクリックし、Title を入力し、Key に 1. で作成した .pub ファイルの中身をペーストし、[ Add SSH Key ] をクリック
![image](https://github.com/user-attachments/assets/bca002c0-6f8b-42b8-883e-ff82f0893462)

4. git config を作成

```
git config --global user.name "your_name"
git config --global user.email "your_email"
```

5. 接続確認

```
$ ssh -T git@github.com
```
以下が表示されたら成功
```
Hi your_name! You've successfully authenticated, but GitHub does not provide shell access.
```
### Git コマンド
#### ブランチ操作
- `git branch`: ブランチ一覧を表示
- `git branch branch_name`: ブランチを作成
- `git branch -d branch_name`: ブランチを削除
- `git branch -m new_branch_name`: 現在のブランチの名前を変更
---
- `git checkout branch_name`: ブランチの切り替え、一時的にそのブランチにいる
- `git checkout -b`: 新規にブランチを作成して切り替える
- `git checkout other_branch -- file_name`: ほかブランチからファイルを復元
---
- `git switch branch_name`: 既存ブランチに切り替え
- `git switch -c branch_name`: 新たにブランチを作成して切り替えをする
- `git switch -c branch_name origin branch_name`: リモートブランチをローカルに持ってくる

#### ステージ
- ファイルの変更をコミットする前に一時的に保存しておく領域
  - 変更を細かく管理できる
  → 例えば、複数のファイルを編集したが、一部だけをコミットしたいときに便利。
  - コミットの粒度をコントロールできる
  → 意図した単位で履歴を残せるため、後から見返しやすい。
  - レビューしやすくなる
  → プルリクエストでの差分が明確になる。
- `git add file_dir`: 特定のファイルをステージに追加
- `git add .`: すべてをステージに追加
- `git status`: 現在のステージング状況を確認
- `git diff`: ステージング前の変更を確認
- `git diff --staged`: ステージング済みの変更を確認

![alt text](image.png)

#### コミット
- Git において「変更内容を記録する操作」== ステージングエリアに追加された変更を、履歴としてリポジトリに保存する
- 粒度が大事：1つのコミットには 1 つの意味を持たせると後で見返しやすい
- `git commit -m "message_text"`: ステージングされた変更をコミット
- `git commit -a -m "message_text"`: ステージングせずに直接コミット(※)

#### リモートブランチ
- リモートブランチ: GitHub 存在するブランチ
- `git push remote_name branch_name`: ローカルリポジトリの変更をリモートリポジトリに反映させる
- `origin`：リモートリポジトリの名前（通常はデフォルトで origin）
- `git push -u origin branch_name`: 追跡ブランチ、以降 `git push` だけで済むようになる


## レポジトリを作成してみよう！
1. [Repositories](https://github.com/your_name?tab=repositories) ページにて、[ New ] ボタンをクリックし、以下の項目を入力

- Repository name
- Description
公開レポジトリかプライベートレポジトリを選択し、README ファイルを追加するか選択して [ Create repository ] をクリック

2. フォルダを作成して実行
```
echo “Hello World" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:<name>/<project>.git
git push -u origin main
```

## レポジトリをクローンしてみよう！
Fork: https://github.com/pyxudev/study
```
git clone git@github.com/<yourname>/study.git
```
`README.md` を含むフォルダが作成されたら成功

## コードのバージョン更新

全体の流れ：ローカル編集 → Stage にコミット → Push する → Pull Request 作成 → コードレビュー → Merge<br>
Pull request は [fork 先 dev] → [dev] → [main] の順番で Mergeされていく

`README.md` の中身を編集してプッシュする
```
git branch -m dev
git add .
git commit -m "<comment>"
git push origin dev
```

直接 main ブランチに push する場合は独自のブランチを作成
```
git branch -m <your_branch>
git add .
git commit -m "<comment>"
git push origin <your_branch>
```

## Pull request を作成

[ Create pull request ] をクリックし、画面遷移後再度 [ Create pull request ] をクリック

## 最新の更新を同期する
```
git remote add true_origin https://github.com/pyxudev/study
git fetch true_origin
git checkout main
git pull true_origin main
```

## そのほかの便利機能など
- 最後のコミットからの修正を退避される
  - `git status`
  - `git stash`
- 修正取り消し
  - `git restore test.txt` / `git checkout test.txt`
    - git checkout は使わない
- リモートを登録し間違えたとき
  - `git remote remove <repo_name>`
- どの行が誰によって修正されたかを確認する
  - `git blame <filename>`
- git bisect start <bad_branch> <current_good_commit>
  - `git bisect good` 問題ないとき
  - `git bisect bad` バグが入っている最初のコミットを特定
- Issue 機能
- GitHub pages で静的サイトを公開
- GitHub Actions で PR を自動化
- GitHub Copilot で学習を加速させよう
