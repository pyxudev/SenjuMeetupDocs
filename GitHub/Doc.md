# GitHub　ハンズオン

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
  - 各ブランチでの作業を一つのブランチに統合する操作。

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

1. SSH キーの生成

Windows: C:\Users\your_usrname\.ssh<br>
Linux: home/.ssh<br>
にて
```
$ ssh-keygen -t ed25519 -C "your_email@example.com"
```

2. SSH キーの追加

[ settings ] → [ SSH and GCP keys ] → [ New SSH Key ] をクリックし、Title を入力し、Key に 1. で生成した .pub ファイルの中身をペーストし、[ Add SSH Key ] をクリック

3. config ファイルの作成

上記 1. の .ssh ディレクトリにて config ファイルを作成し以下を入力
```
Host github
  HostName github.com
  IdentityFile ~/.ssh/your_keyname
  User git
```
4. 接続確認
```
$ ssh -T git@github.com
```
以下が表示されたら成功
```
Hi your_name! You've successfully authenticated, but GitHub does not provide shell access.
```

## レポジトリを作成してみよう！
1. [Repositories](https://github.com/your_name?tab=repositories) ページにて、[ New ] ボタンをクリックし、以下の項目を入力

- Repository name
- Description
公開レポジトリかプライベートレポジトリを選択し、README ファイルを追加するか選択して [ Create repository ] をクリック

2. コードを作成したディレクトリにて以下を実行

```
git init
git git remote add git@github.com:your_name/your_repo.git
git branch -M main
git add .
git commit -m "First commit"
git push origin main
```

## レポジトリをクローンしてみよう！

1. レポジトリのクローン

```
git config --global user.name "your_name"
git config --global user.email "your_email"

git clone git@github.com:pyxudev/study.git
```
`README.md` を含むフォルダが作成されたら成功

## Git のバージョン管理
全体の流れ：ローカル編集 → Stage にコミット → Push する → Pull Request 作成 → コードレビュー → Merge<br>
Pull request は developer → UAT → QA → Prod の順番で Mergeされていく

1. コードのバージョン更新

`README.md` の中身を編集してプッシュする
```
git branch -m dev
git add .
git commit -m "Modified README.md"
git push origin dev
```

2. Pull request を作成

[Pull requests](https://github.com/pyxudev/study/pulls) にて [ New pull request ] をクリックし、`dev` を選択し、[ Create pull request ] をクリックし、画面遷移後再度 [ Create pull request ] をクリック
