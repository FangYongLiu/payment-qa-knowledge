---
id: tbl_payment_tb_refund_limit
object_type: Table
name: tb_refund_limit (tb_refund_limit)
aliases: [tb_refund_limit, payment.tb_refund_limit]
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

# tb_refund_limit (tb_refund_limit)

## 用途
物理表 `payment.tb_refund_limit`,主键 `LIMIT_ID`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `LIMIT_ID` | decimal(32) | 主键ID |
| `RELATION_ORDER_NO` | varchar(32) | 关联订单号 |
| `RELATION_TYPE` | char | 关联订单类型(B-支付订单号/R-关系订单号,组合支付使用) |
| `AVALIABLE_AMOUNT` | decimal(15, 4) | 可用金额 |
| `AVALIABLE_FEE` | decimal(15, 4) | 可用费用 |
| `CURRENCY` | char(3) | 币种 · 可空 |
| `PARTY_ROLE` | varchar(50) | 参与方角色 |
| `MEMBER_ID` | varchar(64) | 会员ID |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFY` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`LIMIT_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
