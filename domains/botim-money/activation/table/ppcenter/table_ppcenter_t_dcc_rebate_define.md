---
id: tbl_ppcenter_t_dcc_rebate_define
object_type: Table
name: DCC rebate template config (t_dcc_rebate_define)
aliases: [t_dcc_rebate_define, ppcenter.t_dcc_rebate_define]
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

# DCC rebate template config (t_dcc_rebate_define)

## 用途
物理表 `ppcenter.t_dcc_rebate_define`,主键 `id`。DCC rebate template config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `config_label` | varchar(128) | Readable label (e.g. USD-AED Rebate 1.5%) |
| `rate` | decimal(10, 6) | Rebate rate |
| `status` | tinyint(1) | 1=Active, 0=Inactive |
| `gmt_create` | timestamp | Rebate define create date |
| `gmt_modify` | timestamp | Rebate define update date |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
