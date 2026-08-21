# Day 08 — branchを作る（2026-08-21）

## やったこと
- 作業開始前に `git pull`（習慣づけ。今日は1人なので変化なし）
- `git branch` でブランチ一覧を確認
- `.git/refs/heads/main` の中身を直接確認
- `git switch -c feature/greeting` でブランチを作成
- 枝の上で1コミット
- 両ブランチの ref ファイルと `git log --oneline` で分岐を確認

## わかったこと
- **ブランチの実体は41バイトのテキストファイル。** `.git/refs/heads/main` の中身は40桁のハッシュ1行だけ。フォルダのコピーではないので、作成は一瞬で容量も増えない
- ブランチを作った直後、**2つのブランチは同じハッシュを指している**。コミットは1つも増えていない
- `git switch` がやっているのは **`.git/HEAD` の指す先を書き換えること**

```
切り替え前 : ref: refs/heads/main
切り替え後 : ref: refs/heads/feature/greeting
```

- **枝の上でコミットすると、その枝だけが進み、`main` は置いていかれる**

```
main              → 15a7e1c   （動かない＝守られている）
feature/greeting  → 80ff6fc   （1つ進んだ）
```

- `git commit` の出力の先頭が `[main ...]` から `[feature/greeting ...]` に変わる。どの枝に入ったかはここで分かる
- `git log --oneline` の括弧が付箋の位置を全部表している

```
80ff6fc (HEAD -> feature/greeting)          ← 自分はここ
15a7e1c (origin/main, origin/HEAD, main)    ← mainとGitHubはここ
```

- 前日は付箋4枚が同じコミットに集まっていた。**分岐すると散らばる**
- `origin/main` が後ろにある＝この枝はまだGitHubに送っていない、という意味

## なぜブランチを使うのか
- `main` を「常に動く安全な状態」として保ったまま、枝の上で自由に試せるから
- 実務では main への直接pushを禁止し、必ず枝＋レビューを通すのが標準

## つまずき
- ターミナルの出力を貼り付ける際に行が入れ替わる事象が続いている。実際の状態は正しかった

## 次回
- Day09 branchを切り替える・mergeする
