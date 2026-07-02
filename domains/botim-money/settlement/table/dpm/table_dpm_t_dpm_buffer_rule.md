---
id: tbl_dpm_t_dpm_buffer_rule
object_type: Table
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (dpm schema) 2026-06-25
tags:
- dpm
- dpm
- t_dpm_buffer_rule
subdomain: dpm
module: null
sensitivity: normal
name: 缓冲入账规则表(t_dpm_buffer_rule)
aliases:
- t_dpm_buffer_rule
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 缓冲入账规则表(t_dpm_buffer_rule)

## 用途
缓冲入账规则表。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `BUFFER_RULE_ID` | decimal(32) | PK / NOT NULL | 缓冲规则ID |
| `PRODUCT_CODE` | varchar(12) | NOT NULL | 产品编码 |
| `PAY_CODE` | varchar(12) | NOT NULL | PE支付编码 |
| `ACCOUNT_NO` | varchar(32) |  | 账户号 |
| `STATUS` | decimal(1) | NOT NULL | 0.有效 1.无效(已删除) |
| `CRDR` | decimal(1) | NOT NULL | 0:双向 1:借 2:贷 |
| `REMARK` | varchar(256) |  | 备注 |
| `CREATE_TIME` | timestamp | NOT NULL | 创建时间 |
| `UPDATE_TIME` | timestamp | NOT NULL | 更新时间 |
| `VALID_TIME` | timestamp | NOT NULL | 生效时间 |
| `UNVALID_TIME` | timestamp | NOT NULL | 失效时间 |

## 主键 / 索引
- 主键:(`BUFFER_RULE_ID`)
- 唯一约束:
  - `UIDX_BUFFER_RULE` 唯一 (PRODUCT_CODE, PAY_CODE, ACCOUNT_NO, CRDR)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
