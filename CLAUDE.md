# CLAUDE.md — municipal-accounting 作業ルール

## 再発防止策（2026-08-08 策定）

### ルール1: 作業開始前に必ず最新 origin/main を確認する

セッション開始時、または編集前に必ず以下を実行:

```bash
git fetch origin
git log --oneline -3 origin/main HEAD
```

ローカルが origin/main より**古い場合** (diverged) は、先に以下でリセットしてから作業:

```bash
git reset --hard origin/main   # 未コミット変更がない場合
# または
git stash && git pull --rebase origin main && git stash pop
```

### ルール2: 変更前に「最新版」を確認してから判断する

ファイルを読む前に必ず `git log --oneline -1 origin/main` で最新コミットを確認し、
ローカルの index.html がその版であることを保証する。

### ルール3: push 前に diverge チェック

```bash
git log --oneline --graph origin/main HEAD -5
```

で分岐がないことを確認してから push。

### ルール4: 古いコミット履歴から判断しない

自分が書いたコードでも、それが古いコミットベースなら**捨てる**。
常に origin/main の最新内容を真とする。

---

## プロジェクト構成

- `index.html` — シングルファイル HTML アプリ（~3000行）
- ローカル開発サーバー: `python -m http.server 8765 --directory .`
- リポジトリ: `zaisei-net/Municipal-Accounting`、ブランチ `main`
