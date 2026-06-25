---
id: tbl_aml_t_aml_info_dd
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (aml schema) 2026-06-25
tags:
- aml
- aml
- t_aml_info_dd
subdomain: aml
module: null
sensitivity: normal
name: 反洗钱搜索结果表(t_aml_info_dd)
aliases:
- t_aml_info_dd
related_services:
- svc_aml
related_scenarios: []
---
# 反洗钱搜索结果表(t_aml_info_dd)

## 用途
反洗钱搜索结果表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键ID |
| `result_id` | bigint |  | 结果集ID |
| `run_id` | bigint |  | 运行ID |
| `entity_name` | varchar(255) |  | 实体名称 |
| `entity_score` | int |  | 得分 |
| `entity_unique_id` | varchar(100) |  | 实体唯一标识符 |
| `category` | varchar(100) |  | 分类 |
| `subcategory` | varchar(150) |  | 实体分类子类 |
| `address_conflict` | tinyint(1) |  | 地址是否冲突 |
| `citizenship_conflict` | tinyint(1) |  | 公民身份是否冲突 |
| `country_conflict` | tinyint(1) |  | 国家是否冲突 |
| `dOB_conflict` | tinyint(1) |  | DOB是否冲突 |
| `entity_type_conflict` | tinyint(1) |  | 实体类型是否冲突 |
| `gender_conflict` | tinyint(1) |  | 性别是否冲突 |
| `id_conflict` | tinyint(1) |  | ID是否冲突 |
| `phone_conflict` | tinyint(1) |  | 电话是否冲突 |
| `real_time_scan_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `country` | varchar(50) |  | 国家 |
| `comments` | text |  | 结果描述 |
| `gender` | tinyint(1) |  | 性别 |
| `dob` | varchar(255) |  | 出生日期 |
| `associations` | text |  | 关联信息 |
| `false_positive` | tinyint(1) |  | falsePositive |
| `true_match` | tinyint(255) |  | trueMatch |
| `member_id` | varchar(50) |  | 会员ID |
| `alert_state` | varchar(10) |  | alert state状态 |
| `user` | varchar(200) |  | 用户名 |
| `division` | varchar(100) |  | Division |
| `risk_level` | tinyint(1) |  | 风险级别 |
| `risk_type` | varchar(32) | 默认 '' | 风险类型 |
| `auto_false_positive` | tinyint(1) |  | autoFalsePositive |
| `create_time` | timestamp | 默认 CURRENT_TIMESTAMP | 数据创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_resultid_entityid` (result_id, entity_unique_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
