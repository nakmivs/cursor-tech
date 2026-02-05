# Git Summary

查看当前 Git 仓库的状态摘要，包括分支信息、最近提交和文件变更。

## 执行步骤

1. 显示当前分支和状态
2. 显示最近 5 条提交记录
3. 显示已修改但未暂存的文件

---

请执行以下命令：

```bash
echo "=== 当前分支 ===" && git branch --show-current && echo "" && echo "=== Git 状态 ===" && git status -s && echo "" && echo "=== 最近 5 条提交 ===" && git log --oneline -5
```

执行完成后，请用中文总结仓库的当前状态。
