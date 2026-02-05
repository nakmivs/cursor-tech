# Git Commit & Push

快速提交所有更改并推送到远端仓库。

---

请按以下步骤执行：

## 1. 查看当前状态

```bash
git status -s && git diff --stat
```

## 2. 暂存所有更改

```bash
git add .
```

## 3. 创建提交

根据更改内容，帮我生成一个简洁的 commit message 并执行提交。提交信息格式要求：
- 使用英文
- 遵循约定式提交（Conventional Commits）：`type: description`
- type 可以是：feat, fix, chore, docs, style, refactor, test, perf
- 不超过 50 个字符

提交命令格式：
```bash
git commit -m "your commit message"
```

## 4. 推送到远端

```bash
git push
```

如果是首次推送该分支，使用：
```bash
git push -u origin HEAD
```

---

执行完成后，请用中文确认提交和推送的结果。
