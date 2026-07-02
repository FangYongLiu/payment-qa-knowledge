---
id: tbl_payment_tb_payment_process
object_type: Table
name: 支付流程 (tb_payment_process)
aliases: [tb_payment_process, payment.tb_payment_process]
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

# 支付流程 (tb_payment_process)

## 用途
物理表 `payment.tb_payment_process`,主键 `PROCESS_ID`。支付流程。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `PROCESS_ID` | bigint | 触发器ID · 可空 |
| `PS_ID` | decimal(15) | 流程配置ID · 可空 |
| `PS_STATE` | char | 支付服务状态 · 可空 |
| `EXPRESSION` | varchar(256) | 执行条件,现在用velocity表达式 · 可空 |
| `IS_ASYN` | char | Y-异步执行,N-同步执行 |
| `GMT_EFFECT` | timestamp | 生效时间 |
| `GMT_EXPIRED` | timestamp | 失效时间，空则代表永不失效 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `NEXT_PS_CODE` | varchar(16) | 下游支付服务编码 · 可空 |

## 主键 / 索引
- 主键:`PROCESS_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
