---
id: tbl_payment_tb_payment_state_mapping
object_type: Table
name: tb_payment_state_mapping (tb_payment_state_mapping)
aliases: [tb_payment_state_mapping, payment.tb_payment_state_mapping]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: payment schema DDL
tags: [payment-core, payment]
sensitivity: normal
related_services: []
---

# tb_payment_state_mapping (tb_payment_state_mapping)

## 用途
物理表 `payment.tb_payment_state_mapping`,主键 `MAPPING_ID`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `MAPPING_ID` | bigint | 主键ID · 可空 |
| `PS_ID` | decimal(15) | 流程配置ID · 可空 |
| `PS_STATE` | char | 支付服务状态 |
| `PAYMENT_STATE` | char | 支付状态 |
| `EXPRESSION` | varchar(256) | 执行条件,现在用velocity表达式 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`MAPPING_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
