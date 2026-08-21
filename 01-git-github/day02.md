# Day 02 — Gitをインストール・設定（2026-08-19）

## やったこと
- `git --version` / `git config --global --list` で現状を確認
- 不足していた3項目を設定
- `ssh -T git@github.com` で GitHub への SSH 認証を確認
- git config のメールアドレスと GitHub 登録メールが一致していることを確認

## 設定した内容
```
git config --global init.defaultBranch main
git config --global core.editor 'code --wait'
git config --global core.quotepath false
```

## わかったこと
- `core.editor` の `--wait` が無いと、Gitがエディタの終了を待たずに空メッセージでコミットを進めてしまう
- `init.defaultBranch main` を設定しておくと、`git init` のたびに master/main の警告が出なくなる
- `core.quotepath false` で日本語ファイル名が `git status` で文字化けしなくなる
- git config のメールが GitHub 登録メールと一致していないと、コミットがプロフィールに紐づかない（草が生えない）

## つまずき
- なし（環境が既に整っていたため前倒しで完了）

## 次回
- Day03 git init / status / add / commit
