---
name: enterprise-data-query
description: 查询企业信息（工商、专利、招投标、财务、风险等）。使用 hqb-data MCP 服务器执行 SQL 查询。当用户询问企业基本信息、股东、专利、招聘、财务数据、风险评估等问题时使用此 skill。
---

# 企业信息查询指南

## 概述

本 skill 指导如何使用 hqb-data MCP 服务器查询企业数据。数据库包含企业工商信息、专利、招投标、财务、风险等多维度数据。

## 核心工具

### 1. exec_query - 执行SQL查询

**重要规则**：SQL 必须使用三段式表名 `catalog.database.table`

```
工具: exec_query
服务器: user-hqb-data
参数:
  - sql: SQL语句（必须使用三段式表名，如 internal.db_name.table_name）
  - max_rows: 返回行数上限，默认100
  - timeout: 超时秒数，默认30
```

### 2. get_table_schema - 获取表结构

查询前先了解表的字段和类型：

```
工具: get_table_schema
服务器: user-hqb-data
参数:
  - table_name: 表名
  - db_name: 数据库名（可选）
```

### 3. get_db_table_list - 列出表清单

```
工具: get_db_table_list
服务器: user-hqb-data
参数:
  - db_name: 数据库名
```

## 查询流程

1. **明确需求**：确定要查询的企业和数据类型
2. **选择表**：根据需求选择合适的表（参考下方表清单或 [tables-reference.md](tables-reference.md)）
3. **了解结构**：如不确定字段，先用 `get_table_schema` 查看
4. **构建SQL**：参考 [sql-examples.md](sql-examples.md) 中的样例
5. **执行查询**：使用 `exec_query` 执行

## 常用表速查

| 领域 | 表名 | 说明 |
|------|------|------|
| 企业基本信息 | `ads_msc_company_info_base` | 工商注册、法人、地址等 |
| 专利信息 | `ads_msc_patent` | 专利申请、授权状态 |
| 招聘信息 | `ads_msc_recruitment_info` | 企业招聘岗位、薪资 |
| 招投标 | `ads_msc_bid_tender_information_rel` | 招投标项目 |
| 财务数据 | `ads_msc_finance_balance` | 资产负债表 |
| 综合风险 | `ads_msc_model_company_risk_total` | 风险评分汇总 |
| 舆情 | `ads_msc_yuqing` | 企业相关舆情 |

完整表清单请参考 [tables-reference.md](tables-reference.md)

### 企业基本信息表常用字段

| 字段名 | 说明 |
|--------|------|
| `company_name` | 企业名称 |
| `legal_rep` | 法定代表人 |
| `regcapital_amt_cal` | 注册资本（元） |
| `found_date` | 成立日期 |
| `business_state` | 经营状态（如"在营（开业）"） |
| `reg_address` | 注册地址 |
| `province` / `city` / `area` | 省/市/区 |
| `industry_nea` | 所属行业 |
| `company_type` | 公司类型 |
| `business_scope` | 经营范围 |
| `uni_code` | 统一社会信用代码 |
| `tel` | 联系电话 |
| `website` | 官方网站 |
| `introduce` | 公司简介 |
| `empnum` | 员工人数 |
| `financing_round` | 融资轮次 |
| `ipo_status` | 上市状态 |

## 快速样例

**查询企业基本信息**：
```sql
SELECT 
  company_name, 
  legal_rep, 
  regcapital_amt_cal, 
  found_date,
  business_state,
  reg_address,
  industry_nea,
  company_type,
  financing_round
FROM internal.ads.ads_msc_company_info_base
WHERE company_name LIKE '%华为%'
LIMIT 10
```

**查询企业专利数量**：
```sql
SELECT patented_person, COUNT(*) as patent_count
FROM internal.ads.ads_msc_patent
WHERE patented_person = '华为技术有限公司'
GROUP BY patented_person
```

更多样例请参考 [sql-examples.md](sql-examples.md)

## 注意事项

1. **表名格式**：必须使用 `catalog.db.table` 三段式，默认 `internal.ads.表名`
2. **性能优化**：大表查询务必添加 `LIMIT`，避免超时
3. **企业名匹配**：精确匹配用 `=`，模糊搜索用 `LIKE '%关键词%'`
4. **数据时效**：数据更新周期不同，查询时注意时间字段
