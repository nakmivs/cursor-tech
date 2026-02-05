# 数据表参考手册

## 表分类索引

### 工商基础类

| 表名 | 说明 | 数据量 |
|------|------|--------|
| ads_msc_company_info_base | 企业基本信息融合表 | ~360万 |
| ads_msc_e_sf_alter | 企业变更信息 | - |
| ads_msc_e_inv_investment | 对外投资 | - |
| ads_msc_an_alterstockinfo | 股东变更信息 | - |
| ads_msc_company_talents_rel | 企业人才关联 | - |

### 知识产权类

| 表名 | 说明 | 数据量 |
|------|------|--------|
| ads_msc_patent | 专利信息 | ~1957万 |
| ads_msc_standard_info | 标准信息 | - |
| ads_msc_domain_record | 域名备案 | - |

### 财务类

| 表名 | 说明 | 数据量 |
|------|------|--------|
| ads_msc_finance_balance | 资产负债表 | - |
| ads_deda_lget_company_revenue_new | 企业营收 | - |

### 招聘招投标类

| 表名 | 说明 | 数据量 |
|------|------|--------|
| ads_msc_recruitment_info | 招聘信息 | - |
| ads_msc_bid_tender_information_rel | 招投标信息 | - |

### 风险类

| 表名 | 说明 | 数据量 |
|------|------|--------|
| ads_msc_model_company_risk_total | 综合风险评分 | - |
| ads_msc_model_company_risk_one | 单项风险明细 | - |
| ads_msc_judge_doc_rel | 裁判文书 | - |
| ads_msc_court_announcement_rel | 法院公告 | - |
| ads_msc_ktgg | 开庭公告 | - |
| ads_msc_zxgk_zhixing_data | 被执行人 | - |
| ads_msc_bond_default | 债券违约 | - |
| ads_msc_tax_illegal | 税务违法 | - |

### 舆情类

| 表名 | 说明 | 数据量 |
|------|------|--------|
| ads_msc_yuqing | 企业舆情 | - |
| ads_msc_yuqing_rel | 舆情关联 | - |

### 资质认证类

| 表名 | 说明 | 数据量 |
|------|------|--------|
| ads_msc_tax_level | 纳税信用等级 | - |
| ads_msc_tax_qualification | 税务资质 | - |
| ads_msc_construction_ent_qualification | 建筑企业资质 | - |
| ads_msc_regulated_company | 监管企业 | - |
| ads_msc_gazelle_company | 瞪羚企业 | - |
| ads_msc_innovation_company | 创新型企业 | - |

### 其他

| 表名 | 说明 | 数据量 |
|------|------|--------|
| ads_msc_customs_reg_ent | 海关登记企业 | - |
| ads_msc_land_information_rel | 土地信息 | - |
| ads_msc_judicial_auction | 司法拍卖 | - |
| ads_msc_industral_chain_ent | 产业链企业 | - |

---

## 详细表结构

> 💡 使用 `get_table_schema` 工具可获取任意表的完整字段信息

### ads_msc_company_info_base

**说明**：公司基础信息融合表，包含工商注册的核心信息

| 字段名 | 类型 | 说明 |
|--------|------|------|
| company_name | VARCHAR(500) | 企业名称 |
| legal_rep | VARCHAR(500) | 法定代表人 |
| regcapital_amt_cal | DECIMAL(15,2) | 注册资本（万元） |
| found_date | DATE | 成立日期 |
| reg_address | TEXT | 注册地址 |
| business_scope | TEXT | 经营范围 |
| uni_code | VARCHAR(50) | 统一社会信用代码 |
| business_state | VARCHAR(50) | 企业状态 |
| eid | VARCHAR(64) | 企业ID |
| province | VARCHAR(50) | 省份 |
| city | VARCHAR(50) | 城市 |
| industry_nea | VARCHAR(255) | 行业分类 |

---

### ads_msc_patent

**说明**：专利信息表

| 字段名 | 类型 | 说明 |
|--------|------|------|
| patented_person | TEXT | 专利权人/企业名称 |
| patent_name | VARCHAR(600) | 专利名称 |
| type_name | VARCHAR(60) | 专利类型（发明/实用新型/外观设计） |
| request_date | DATE | 申请日期 |
| request_num | VARCHAR(150) | 申请号 |
| outhor_date | DATE | 授权日期 |
| outhor_num | VARCHAR(150) | 授权公告号 |
| law_state | TEXT | 法律状态 |
| inventor | TEXT | 发明人 |
| brief | TEXT | 摘要 |

---

## 字段补充说明

（随使用过程逐步补充各表的业务字段含义）

### 常见字段命名规律

| 后缀/关键词 | 含义 |
|------------|------|
| `_date` | 日期类型 |
| `_time` | 时间戳 |
| `_rel` | 关联表 |
| `company_name` / `entname` | 企业名称（常用关联字段） |
| `uni_code` | 统一社会信用代码（唯一标识） |
| `eid` | 企业ID（内部唯一标识，用于关联查询） |
| `legal_rep` | 法定代表人 |
| `found_date` | 成立日期 |
| `business_state` | 经营状态 |
