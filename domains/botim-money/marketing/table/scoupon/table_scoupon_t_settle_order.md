---
id: tbl_scoupon_t_settle_order
object_type: Table
name: 结算订单表 (t_settle_order)
aliases: [t_settle_order, scoupon.t_settle_order]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: scoupon schema DDL
tags: [marketing, scoupon]
sensitivity: normal
related_services: []
---

# 结算订单表 (t_settle_order)

## 用途
物理表 `scoupon.t_settle_order`,主键 `voucher_no`。结算订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `voucher_no` | bigint(17) | 结算订单 |
| `record_id` | bigint(17) | 记录ID |
| `biz_product_code` | varchar(8) | 业务产品码 |
| `payer_mid` | varchar(32) | 付款人ID |
| `payer_acct_type` | varchar(32) | 付款人账户类型 |
| `merchant_id` | varchar(32) | 商户ID |
| `payee_mid` | varchar(32) | 收款人ID |
| `payee_acct_type` | varchar(32) | 收款人账户类型 |
| `settle_amount` | decimal(15, 4) | 结算金额 |
| `currency` | char(3) | 币种 |
| `status` | varchar(8) | 状态 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |
| `unity_result_code` | varchar(100) | 错误码 · 可空 |
| `extension` | varchar(512) | 扩展参数 · 可空 |

## 主键 / 索引
- 主键:`voucher_no`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
