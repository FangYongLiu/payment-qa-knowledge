---
id: tbl_payment_tb_cs_agreement
object_type: Table
name: 清结算协议 (tb_cs_agreement)
aliases: [tb_cs_agreement, payment.tb_cs_agreement]
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

# 清结算协议 (tb_cs_agreement)

## 用途
物理表 `payment.tb_cs_agreement`,主键 `AGREEMENT_ID`。清结算协议。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `AGREEMENT_ID` | bigint | 协议ID，主键:SEQ_CLEARING_AGREEMENT · 可空 |
| `PRODUCT_CODE` | varchar(16) | 产品码 |
| `EXECUTE_EXPRESSION` | varchar(512) | 执行表达式 · 可空 |
| `PRIORITY` | decimal(5) | 优先级 |
| `GMT_EFFECT` | timestamp | 生效时间 |
| `GMT_EXPIRED` | timestamp | 失效时间，空则代表永不失效 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `BIZ_PRODUCT_CODE` | varchar(16) | 业务产品编码 · 可空 |

## 主键 / 索引
- 主键:`AGREEMENT_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
