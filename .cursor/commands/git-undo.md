# Git Undo

撤销操作工具集，安全回退代码。

---

请先告诉我你想要撤销什么操作，然后我会选择合适的命令：

## 选项 A：撤销暂存（已 add 但未 commit）

恢复到工作区，不丢失修改：
```bash
git restore --staged .
```

## 选项 B：撤销工作区的修改

⚠️ **危险**：会丢失所有未提交的修改
```bash
git restore .
```

## 选项 C：撤销最后一次提交

保留修改在工作区：
```bash
git reset --soft HEAD~1
```

完全删除最后一次提交和修改：
```bash
git reset --hard HEAD~1
```

## 选项 D：撤销已推送的提交

查看最近提交记录：
```bash
git log --oneline -5
```

创建一个反向提交（安全方式）：
```bash
git revert commit-hash
```

---

执行前我会再次确认操作，避免误删代码。
