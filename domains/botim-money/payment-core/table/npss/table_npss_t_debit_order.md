---
id: tbl_npss_t_debit_order
object_type: Table
name: idsct唯一索引 (t_debit_order)
aliases: [t_debit_order, npss.t_debit_order]
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

# idsct唯一索引 (t_debit_order)

## 用途
物理表 `npss.t_debit_order`,主键 `trx_voucher_no`。idsct唯一索引。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `trx_voucher_no` | bigint | 借记凭证 凭证服务产生 |
| `message_id` | bigint | 消息id |
| `comm_type` | char(4) | 访问类型,api-接口,sftp · 可空 |
| `debit_order_type` | varchar(10) | 借记交易类型， · 可空 |
| `member_id` | varchar(20) | 会员id · 可空 |
| `amount` | decimal(19, 4) | 金额 |
| `currency` | char(3) | 币种 |
| `transfer_amount` | decimal(19, 4) | 转账金额 |
| `fee_amount` | decimal(19, 4) | 手续费金额 |
| `status` | char | 状态, I-初始,P-支付,S-成功,F-失败,E-异常,R-已退款 |
| `transfer_type` | char(3) | 转账类型,I2I-内转内,I2O-内转外,O2I-外转内 · 可空 |
| `pb_type` | char | personal or business: P/B |
| `dr_type` | char | debit or refund: D/R |
| `id_sct` | varchar(32) | 银行订单号 |
| `inner_order_no` | varchar(50) | Inner Order No · 可空 |
| `debit_phase` | char(2) | Debit Phase, enums: CT-Create Transaction, P8-Pacs.008 sent, P2-Pacs.002 Received · 可空 |
| `need_bill` | char | If Send Bill, Y-Send, N-Not Send · 可空 |
| `dbtr_bic` | varchar(11) | 付款方银行编码 · 可空 |
| `cdtr_bic` | varchar(11) | 收款方银行编码 · 可空 |
| `instruct_id` | varchar(35) | 指令id · 可空 |
| `source` | varchar(10) | 来源,payby-payby支付;other-其他支付 · 可空 |
| `response_code` | varchar(10) | 银行响应码 · 可空 |
| `unity_result_code` | varchar(64) | 同意结果 · 可空 |
| `extension` | varchar(512) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `gmt_create` | timestamp(3) | create time |
| `gmt_modified` | timestamp(3) | modify time · 可空 |
| `gmt_finished` | timestamp(3) | finish time · 可空 |

## 主键 / 索引
- 主键:`trx_voucher_no`
- `idx_do_member_modified`:member_id, gmt_modified

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
