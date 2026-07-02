---
id: tbl_npss_t_credit_order
object_type: Table
name: 贷记订单表 (t_credit_order)
aliases: [t_credit_order, npss.t_credit_order]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: npss schema DDL
tags: [payment-core, npss]
sensitivity: normal
related_services: []
---

# 贷记订单表 (t_credit_order)

## 用途
物理表 `npss.t_credit_order`,主键 `trx_voucher_no`。贷记订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `trx_voucher_no` | bigint | 贷记凭证 凭证服务产生 · 可空 |
| `message_id` | bigint | 消息id |
| `product_order_no` | bigint | 交易凭证号 · 可空 |
| `comm_type` | char(4) | 访问类型，api-接口,sftp · 可空 |
| `credit_order_type` | varchar(10) | 贷记交易类型， · 可空 |
| `member_id` | varchar(20) | 会员id |
| `amount` | decimal(19, 4) | 金额 |
| `currency` | char(3) | 币种 |
| `status` | char | 状态 |
| `transfer_type` | char(3) | 转账类型,I2I-内转内,I2O-内转外,O2I-外转内 · 可空 |
| `id_sct` | varchar(64) | Bank Order No · 可空 |
| `need_bill` | char | If Send Bill, Y-Send, N-Not Send · 可空 |
| `dbtr_bic` | varchar(11) | 付款方银行编码 · 可空 |
| `instruct_id` | varchar(35) | 指令id · 可空 |
| `retry_voucher_no` | bigint | Retry Voucher No · 可空 |
| `unity_result_code` | varchar(64) | 同意结果 · 可空 |
| `extension` | varchar(512) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `gmt_finished` | timestamp | 结束时间 · 可空 |

## 主键 / 索引
- 主键:`trx_voucher_no`
- `uk_co_idsct`:id_sct (UNIQUE)
- `uk_co_instructed_id`:instruct_id (UNIQUE)
- `idx_co_gmt_modified`:gmt_modified, member_id
- `idx_co_retry_voucher_no`:retry_voucher_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
