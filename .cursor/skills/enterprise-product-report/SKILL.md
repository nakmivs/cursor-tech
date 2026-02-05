---
name: enterprise-product-report
description: 生成企业产品报告。使用 mitaso MCP 搜索企业产品信息并输出 markdown 报告。当用户需要了解某企业的产品、服务、解决方案时使用此 skill。
---

# 企业产品报告生成

## 概述

使用 mitaso MCP 工具搜索企业产品信息，按照固定模板生成 markdown 报告文件。

## 工具说明

使用 `user-mitaso` 服务器的工具：

### metaso_web_search - 搜索产品信息

```
服务器: user-mitaso
工具: metaso_web_search
参数:
  - q: 搜索关键词（如 "华为 产品"）
  - size: 返回数量（建议 10）
  - scope: "webpage"
  - includeSummary: true
```

### metaso_web_reader - 读取页面详情

```
服务器: user-mitaso
工具: metaso_web_reader
参数:
  - url: 页面地址
  - format: "markdown"
```

## 工作流程

1. 获取企业名称
2. 使用 `metaso_web_search` 搜索 "{企业名称} 产品 服务"
3. 从搜索结果中选取 2-3 个关键页面，用 `metaso_web_reader` 读取详情
4. 按照下方模板整理信息
5. 输出到 `docs/reports/{企业名称}-产品报告.md`

## 报告模板

```markdown
# {企业名称} 产品报告

> 生成时间: {日期}

## 企业概述

{企业简介，1-2 段}

## 核心产品

### {产品1名称}
{产品描述}

### {产品2名称}
{产品描述}

（根据搜索结果添加更多产品）

## 产品特点

- {特点1}
- {特点2}
- {特点3}

## 信息来源

- [{来源标题1}]({URL1})
- [{来源标题2}]({URL2})
```

## 注意事项

1. 输出目录固定为 `docs/reports/`，如目录不存在需先创建
2. 文件名格式：`{企业名称}-产品报告.md`
3. 信息来源必须列出，确保可追溯
