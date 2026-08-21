# Day 04 — log・diff・restore（2026-08-20）

## やったこと
- `git log`（フル表示）で ハッシュ40桁 / Author / 日時 / メッセージ を確認
- `git log --oneline` で1行表示
- ファイルに1行追記して `git diff`
- `git add` してから、もう一度 `git diff`
- `git diff --staged`
- わざと間違った行を追記し、`git restore` で破棄

## わかったこと
- **2つの diff は見ている場所が違う**

```
ワークツリー ──git diff──> ステージ ──git diff --staged──> 最後のコミット
```

- `git add` した直後に `git diff` が**空になる**のは、ワークツリーとステージが一致したから。変更が消えたわけではなく `git diff --staged` に移っている
- Day03で見た `MM` は「この2つの diff が別々の中身を持っている状態」だった
- diff の読み方は行頭の記号だけ見ればよい。`+` が追加、`-` が削除、空白は変更なし
- **`git restore` と `git restore --staged` は名前が似ているが別物**

| コマンド | 動作 | 危険度 |
|---|---|---|
| `git restore ファイル名` | ワークツリーの変更を**捨てる** | 高（戻せない） |
| `git restore --staged ファイル名` | ステージから**降ろすだけ** | 低（ファイルは無事） |

- コミットしていない変更はGitのどこにも記録がないので、`git restore` で消したものは復元できない

## つまずき
- なし

## 次回
- Day05 GitHubリポジトリを作る
