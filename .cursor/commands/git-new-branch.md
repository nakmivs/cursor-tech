# Git New Branch

从 main 分支创建新的功能分支。

---

## 1. 切换到 main 分支并拉取最新代码

```bash
git switch main && git pull
```

## 2. 创建并切换到新分支

请询问我要创建的分支名称，然后执行：

```bash
git switch -c branch-name
```

分支命名建议：
- `feature/功能名` - 新功能开发
- `fix/问题描述` - Bug 修复
- `refactor/重构内容` - 代码重构
- `docs/文档更新` - 文档更新

## 3. 首次推送分支

```bash
git push -u origin HEAD
```

---

执行完成后，请用中文确认分支创建成功。
