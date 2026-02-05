# Git Sync

同步远端最新代码到本地分支。

---

## 1. 查看当前状态

```bash
git status -s
```

如果有未提交的更改，请先决定是否需要提交或暂存。

## 2. 拉取远端更新

如果工作区干净：
```bash
git pull
```

如果有未提交的更改，使用 stash 暂存：
```bash
git stash && git pull && git stash pop
```

## 3. 如果需要从 main 合并最新代码

```bash
git fetch origin main && git merge origin/main
```

或使用 rebase（保持提交历史整洁）：
```bash
git fetch origin main && git rebase origin/main
```

---

执行完成后，我会告诉你是否有冲突需要解决。
