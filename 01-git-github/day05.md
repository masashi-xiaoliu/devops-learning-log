# Day 05 — GitHubリポジトリを作る（2026-08-20）

## やったこと
- GitHub で練習用リポジトリを **Private・README等チェックなし**で作成
- `git remote add origin git@github.com:<ユーザー名>/<リポジトリ名>.git` で接続
- `git remote -v` で確認

## わかったこと
- **リポジトリの作り方は2通りあり、状況で使い分ける**

| 状況 | 作り方 |
|---|---|
| 手元に既にコードがある | GitHub側は**空**で作り、`git remote add` で後から繋ぐ |
| ゼロから始める | GitHub側で **README等を入れて**作り、`git clone` する（今後の主流） |

- 手元に履歴があるのに GitHub 側でも README を作らせると、親子関係のない履歴が2本できてしまい、繋ぐときに面倒になる
- `origin` はリモートに付ける**あだ名**。慣習でそう呼んでいるだけで、別名でも動く
- `git remote -v` が fetch / push の2行を出すのは、取得先と送信先を別々に設定できるから
- **`git remote add` の時点ではまだ一度も通信していない。** 設定を書いただけ

## つまずき
- なし

## 次回
- Day06 push / pull
