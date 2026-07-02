---
id: tbl_sme_t_loan_order_contract
object_type: Table
name: t_loan_order_contract (t_loan_order_contract)
aliases: [t_loan_order_contract, sme.t_loan_order_contract]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: sme schema DDL
tags: [lending, sme]
sensitivity: normal
related_services: []
---

# t_loan_order_contract (t_loan_order_contract)

## 用途
物理表 `sme.t_loan_order_contract`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(10) | 待补 · 可空 |
| `contract_no` | varchar(64) | Internally generated contract number |
| `contract_type` | varchar(32) | Protocol type |
| `loan_order_no` | varchar(64) | order_no in table t_loan_order |
| `signed_time` | timestamp | Time of signing |
| `file_tag` | varchar(128) | Path where the contract file is saved in the ufs system · 可空 |
| `create_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `ix_ct`:create_time
- `ix_no`:contract_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
