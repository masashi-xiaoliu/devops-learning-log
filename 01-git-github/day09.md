# Day 09 — branchを切り替える・mergeする（2026-08-21）

## やったこと
- `feature/greeting` で `cat src/main.py`（3行ある状態を確認）
- `git switch main` → **「こんにちは」の行が消える**
- `git switch feature/greeting` → 復活する。往復して確認
- `main` に戻って `git merge feature/greeting`
- `git push` で GitHub の `main` を更新
- `git branch -d feature/greeting` で枝を削除

## わかったこと

### `git switch` は「ファイルを並べ替える」動作

ブランチを切り替えると、そのブランチが指すコミットのスナップショットどおりにワークツリーが書き戻される。
**ファイルが消えたのではなく、そのときの姿に戻っただけ。**

```
main が指す 15a7e1c のスナップショット → 「こんにちは」は入っていない
feature/greeting が指す 80ff6fc       → 入っている
```

Day01 で学んだ「コミット＝その時点の写真」が、ここで実感として繋がった。
アルバムのページをめくると、その写真どおりに机の上が並べ替えられるイメージ。

### merge は「取り込む側」に立ってから実行する

`main` に取り込みたいので、先に `git switch main` してから `git merge feature/greeting`。
逆にすると、枝の側に main を取り込むことになる。

### Fast-forward

```
Updating 15a7e1c..80ff6fc
Fast-forward
```

`main` は枝を切ってから一歩も動いていなかったので、**新しいコミットを作る必要がなく、付箋を滑らせるだけで済んだ**。
Day06 の `git pull` で見たのと同じ言葉。同じ仕組みだった。

```
合流前   15a7e1c ──> 80ff6fc          合流後   15a7e1c ──> 80ff6fc
            ↑           ↑                                     ↑
          main    feature/greeting                    main と feature/greeting
```

### merge はローカルの操作

merge した直後の `git log --oneline`：

```
80ff6fc (HEAD -> main, feature/greeting)   ← main が追いついた
15a7e1c (origin/main, origin/HEAD)         ← GitHubだけ取り残されている
```

**GitHubは何も知らない。** `git push` して初めて反映される。

### ブランチを削除してもコミットは消えない

```
$ git branch -d feature/greeting
Deleted branch feature/greeting (was 80ff6fc).

$ git log --oneline
80ff6fc (HEAD -> main, origin/main, origin/HEAD) 挨拶をもう1行追加   ← 残っている
```

消えたのは**付箋だけ**。Day01の「ブランチはただのラベル」が、削除しても実害がないという形で確認できた。
`-d` には安全装置があり、まだマージしていない枝を消そうとすると拒否される。

## 一周できたこと

```
枝を切る → 作業する → 合流する → 片付ける
```

## 次回への伏線
実務では `main` への直接 merge / push は禁止されていることが多い。
代わりに **Pull Request** を出してレビューを受ける。Day10 でその流れをやる。

```
今日      枝で作業 → 自分で main に merge
実務      枝で作業 → GitHubにpush → PRを出す → レビュー → merge
```

## つまずき
- 説明文をコマンドと勘違いして実行し `fatal: only one reference expected` が出た。害はなし

## 次回
- Day10 GitHubでPull Requestを作る
