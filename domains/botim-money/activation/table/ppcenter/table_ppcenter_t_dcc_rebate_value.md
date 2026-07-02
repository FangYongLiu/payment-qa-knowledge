---
id: tbl_ppcenter_t_dcc_rebate_value
object_type: Table
name: Merchant-specific DCC rebate values (t_dcc_rebate_value)
aliases: [t_dcc_rebate_value, ppcenter.t_dcc_rebate_value]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppcenter schema DDL
tags: [activation, ppcenter]
sensitivity: normal
related_services: []
---

# Merchant-specific DCC rebate values (t_dcc_rebate_value)

## 用途
物理表 `ppcenter.t_dcc_rebate_value`,主键 `id`。Merchant-specific DCC rebate values。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `rate` | decimal(10, 6) | Rebate rate |
| `gmt_effective` | timestamp | Effective time · 可空 |
| `gmt_invalid` | timestamp | Expiry time (set on deactivation) · 可空 |
| `gmt_create` | timestamp | Rebate value create date |
| `gmt_modify` | timestamp | Rebate value update date |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
