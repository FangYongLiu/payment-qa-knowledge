---
id: tbl_aml_t_member_risk_rate_his
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
- t_member_risk_rate_his
subdomain: aml
module: null
sensitivity: normal
name: 会员风险评级历史(t_member_risk_rate_his)
aliases:
- t_member_risk_rate_his
related_services:
- svc_aml
related_scenarios: []
---
# 会员风险评级历史(t_member_risk_rate_his)

## 用途
会员风险评级历史。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `member_id` | varchar(20) | NOT NULL | 会员id |
| `risk_rate_score` | decimal(19,4) | NOT NULL | 风险评级分数 |
| `risk_rating` | varchar(10) | NOT NULL | 风险等级 |
| `risk_rate_date` | timestamp(3) | NOT NULL | 风险评级时间 |
| `params` | varchar(500) | NOT NULL | 执行参数 |
| `checked` | char | NOT NULL | 是否已完成审核(Y/N) |
| `status` | char(2) |  | 状态 |
| `scan_date` | timestamp |  | 最近一次扫描LN的时间 |
| `create_time` | timestamp(3) | NOT NULL | 创建时间 |
| `update_time` | timestamp(3) | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_member_id` (member_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
