
1. clone <repo>
2. repo をvaultに指定
3. *2の後、* Community Plugins の Git をいれて有効化
4. ここでは自動プッシュはしないでGUIでstage,commit,pushすることに。右サイドパネルからできる
5. pushがうまくいかない
```sh
% git pull
hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before
hint: your next pull:
hint:
hint:   git config pull.rebase false  # merge
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint:
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
fatal: Need to specify how to reconcile divergent branches.
```

`git config pull.rebase true` で解決。


---

gptさんメモ

## 選択肢は3つ

### ① merge（マージ）

`git pull --no-rebase` または `git config pull.rebase false`

**特徴**
- マージコミットが作られる
- 履歴が分岐して残る

**向いているケース**
- チーム開発
- 履歴をそのまま残したい

### ② rebase（おすすめ）

`git pull --rebase` または `git config pull.rebase true`

**特徴**
- 自分のコミットを最新のリモートの上に載せ直す
- 履歴が一直線でキレイ

**向いているケース**
- 個人開発 
- feature ブランチ
- きれいな履歴が好き

👉 多くの人がこれを使っています。

### ③ fast-forward only（厳しめ）

`git pull --ff-only` または `git config pull.ff only`

**特徴**
- 分岐していたら pull 失敗
- 勝手なマージが起きない

**向いているケース**
- 安全第一
- 自分で必ず判断したい人
