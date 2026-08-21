# Day 06 — push・pullを使う（2026-08-20）

## やったこと
- `git push -u origin main` で初回 push
- GitHub の画面でファイル一覧を確認
- GitHub 上で README を直接編集（同僚役）してコミット
- ローカルで `git status` → `git pull`
- `git log --oneline` で状態を確認

## わかったこと
- `-u` は「この組み合わせを既定にする」指定。**次回から `git push` だけでよくなる**
- push の出力に出る `Delta compression` は、保存時の差分圧縮。**コミットの考え方はスナップショットだが、ディスクに書く層では差分も使っている**（Day01の補足の実物）
- **未追跡ファイルは push されない。** GitHub の画面に `.env` が無いことを確認できた。Day03 でファイルを個別に `git add` していたことが効いた
- GitHub 側を更新した後でも、ローカルの `git status` は **`Your branch is up to date` と表示する（嘘をつく）**
  - Gitは自動でリモートを見に行かない。表示は**最後に通信したときの記憶**との比較
  - 通信するのは `push` / `pull` / `fetch` / `clone` のときだけ
- `Fast-forward` は「手元に独自のコミットが無かったので、先頭を進めるだけで済んだ」という意味
- `git log --oneline` の `(HEAD -> main, origin/main)` は**付箋が3枚同じコミットに貼られている**状態＝ローカルとリモートが完全一致

## 気づいたこと（実務ルール）
- **チーム作業では作業開始前に `git pull` する。** 古い状態の上に作業を積むとコンフリクトが起きやすい
- push 直前にも pull すると安全。`! [rejected] ... (fetch first)` は「先に取ってこい」の意味
- Day08 以降ブランチを使い始めたら、**ブランチを切る前に main を pull する**形になる

## つまずき
- なし

## 次回
- Day07 .gitignore
