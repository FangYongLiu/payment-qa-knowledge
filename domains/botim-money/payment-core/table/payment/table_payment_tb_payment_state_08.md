---
id: tbl_payment_tb_payment_state_08
object_type: Table
name: tb_payment_state_08 (tb_payment_state_08)
aliases: [tb_payment_state_08, payment.tb_payment_state_08]
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

# tb_payment_state_08 (tb_payment_state_08)

## 用途
物理表 `payment.tb_payment_state_08`,主键 `PAYMENT_SEQ_NO`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `PAYMENT_SEQ_NO` | varchar(32) | YYYYMMDD||CODE[2]||SEQ_PAYMENT_ORDER[8] |
| `PS_ID` | decimal(15) | 流程配置ID · 可空 |
| `PAYMENT_STATE` | char | S-成功,F-失败,P-处理中 |
| `PS_STATE` | char | S-成功,F-失败,P-处理中 |
| `PRE_PS_ID` | decimal(15) | 前支付服务ID · 可空 |
| `PRE_PS_STATE` | char | S-成功,F-失败,P-处理中 · 可空 |
| `PAUSE_TAG` | varchar(16) | 暂停标记 · 可空 |
| `REFUNDED` | char | 是否已发起退款 · 可空 |
| `NOTIFY_STATUS` | char | Y-已通知 其他为未通知 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`PAYMENT_SEQ_NO`
- `IDX_PS_GMTMODIFIED_08`:GMT_MODIFIED

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
