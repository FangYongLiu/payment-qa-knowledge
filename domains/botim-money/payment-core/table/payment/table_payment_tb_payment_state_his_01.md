---
id: tbl_payment_tb_payment_state_his_01
object_type: Table
name: 记录支付状态的跃迁历史 (tb_payment_state_his_01)
aliases: [tb_payment_state_his_01, payment.tb_payment_state_his_01]
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

# 记录支付状态的跃迁历史 (tb_payment_state_his_01)

## 用途
物理表 `payment.tb_payment_state_his_01`,主键 `HIS_ID`。记录支付状态的跃迁历史。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `HIS_ID` | decimal(18) | 主键 |
| `PAYMENT_SEQ_NO` | varchar(32) | YYYYMMDD||CODE[2]||SEQ_PAYMENT_ORDER[8] |
| `PAYMENT_STATE` | char | 支付状态 |
| `PS_ID` | decimal(15) | 流程配置ID |
| `PS_CODE` | varchar(16) | 当前支付服务编码 |
| `PS_STATE` | char | 当前支付服务状态 |
| `PRE_PS_CODE` | varchar(16) | 前支付服务编码 · 可空 |
| `PRE_PS_STATE` | char | 前支付服务状态 · 可空 |
| `PAUSE_TAG` | varchar(16) | 暂停标记 · 可空 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |

## 主键 / 索引
- 主键:`HIS_ID`
- `IDX_PAYMENT_STATE_HIS_PSN_01`:PAYMENT_SEQ_NO

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
