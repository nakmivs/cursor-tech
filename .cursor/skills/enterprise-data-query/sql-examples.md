# 企业信息查询 SQL 样例

本文档按领域整理常用查询SQL，可直接复用或修改。

---

## 1. 企业基本信息

### 1.1 按企业名称精确查询

```sql
SELECT 
  company_name,
  legal_rep,
  regcapital_amt_cal,
  found_date,
  reg_address,
  business_scope
FROM internal.ads.ads_msc_company_info_base
WHERE company_name = '腾讯科技（深圳）有限公司'
```

### 1.2 按企业名称模糊搜索

```sql
SELECT company_name, legal_rep, found_date
FROM internal.ads.ads_msc_company_info_base
WHERE company_name LIKE '%字节跳动%'
LIMIT 20
```

### 1.3 按地区筛选企业

```sql
SELECT company_name, reg_address
FROM internal.ads.ads_msc_company_info_base
WHERE reg_address LIKE '%深圳市%'
LIMIT 50
```

---

## 2. 专利信息

### 2.1 查询企业专利列表

```sql
SELECT 
  patent_name,
  type_name,
  request_date,
  outhor_date,
  law_state
FROM internal.ads.ads_msc_patent
WHERE patented_person LIKE '%华为技术有限公司%'
ORDER BY request_date DESC
LIMIT 50
```

### 2.2 统计企业专利数量（按类型）

```sql
SELECT 
  patented_person,
  type_name,
  COUNT(*) as count
FROM internal.ads.ads_msc_patent
WHERE patented_person LIKE '%华为技术有限公司%'
GROUP BY patented_person, type_name
```

---

## 3. 招聘信息

### 3.1 查询企业招聘岗位

```sql
SELECT 
  job_title,
  salary_lower,
  salary_upper,
  city,
  publish_date
FROM internal.ads.ads_msc_recruitment_info
WHERE entname LIKE '%阿里巴巴%'
ORDER BY publish_date DESC
LIMIT 30
```

---

## 4. 招投标

### 4.1 查询企业中标项目

```sql
SELECT 
  subject_name,
  bid_price,
  bid_address,
  bid_type,
  create_time
FROM internal.ads.ads_msc_bid_tender_information_rel
WHERE subject_name LIKE '%中国建筑%'
ORDER BY create_time DESC
LIMIT 30
```

---

## 5. 风险数据

### 5.1 查询企业综合风险评分

```sql
SELECT 
  r.eid,
  r.risk_rank,
  r.update_time,
  c.company_name
FROM internal.ads.ads_msc_model_company_risk_total r
LEFT JOIN internal.ads.ads_msc_company_info_base c ON r.eid = c.eid
WHERE c.company_name = '某某公司'
```

---

## 6. 关联查询（进阶）

### 6.1 企业基本信息 + 专利数量

```sql
SELECT 
  a.company_name,
  a.legal_rep,
  a.found_date,
  COUNT(b.patent_name) as patent_count
FROM internal.ads.ads_msc_company_info_base a
LEFT JOIN internal.ads.ads_msc_patent b 
  ON b.patented_person LIKE CONCAT('%', a.company_name, '%')
WHERE a.company_name = '腾讯科技（深圳）有限公司'
GROUP BY a.company_name, a.legal_rep, a.found_date
```

---

## 添加新样例的格式

请按以下格式添加新的SQL样例：

```markdown
### X.X 样例标题
**场景说明**：简述什么情况下使用（可选）

\```sql
-- 你的SQL
SELECT ...
\```
```
