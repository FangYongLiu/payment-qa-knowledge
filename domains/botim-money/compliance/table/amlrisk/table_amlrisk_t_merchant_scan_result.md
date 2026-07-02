---
id: tbl_amlrisk_t_merchant_scan_result
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (amlrisk schema) 2026-06-25
tags:
- amlrisk
- amlrisk
- t_merchant_scan_result
subdomain: amlrisk
module: null
sensitivity: normal
name: 商户扫描结果表(t_merchant_scan_result)
aliases:
- t_merchant_scan_result
related_services:
- svc_aml
related_scenarios: []
---
# 商户扫描结果表(t_merchant_scan_result)

## 用途
商户扫描结果表。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `merchant_info_id` | bigint |  | 商户信息id |
| `screen_result` | varchar(2000) |  | 扫描结果（json） |
| `risk_assessment` | varchar(2000) |  | 评级结果（json） |
| `CREATED_TIME` | timestamp |  | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
