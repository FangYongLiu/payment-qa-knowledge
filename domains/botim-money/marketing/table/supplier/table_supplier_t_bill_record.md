---
id: tbl_supplier_t_bill_record
object_type: Table
name: 账单记录表 (t_bill_record)
aliases: [t_bill_record, supplier.t_bill_record]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: supplier schema DDL
tags: [marketing, supplier]
sensitivity: normal
related_services: []
---

# 账单记录表 (t_bill_record)

## 用途
物理表 `supplier.t_bill_record`,主键 `id`。账单记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(32) | id |
| `member_id` | varchar(16) | 会员编号 |
| `SUPPLIER_CHANNEL_CODE` | varchar(32) | 渠道编号 |
| `PROVIDER_CODE` | varchar(32) | 供应商编号 |
| `PROVIDER_NAME` | varchar(32) | 供应商姓名 |
| `PRODUCT_CODE` | varchar(32) | 产品编号 |
| `target_account_no` | varchar(64) | 用户账号 |
| `order_currency` | varchar(3) | 订单币种 |
| `settlement_currency` | varchar(3) | 结算币种 |
| `bill_amount` | decimal(15, 4) | 账单金额 · 可空 |
| `total_bill_amount` | decimal(15, 4) | 总账单金额 · 可空 |
| `total_bill_sum` | varchar(4) | 总账单数量 · 可空 |
| `STATUS` | varchar(16) | 是否已支付：TRADE_FINISH(交易结束), PROCESSING(交易处理中) |
| `indicative_fx_rate` | decimal(15, 4) | 费率 · 可空 |
| `output_info` | varchar(1024) | 账单详情 · 可空 |
| `inst_transaction_id` | varchar(64) | 合作方对应单号 · 可空 |
| `inst_resp_code` | varchar(32) | 合作方响应码 · 可空 |
| `customer_name` | varchar(64) | 客户名称 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 · 可空 |
| `pay_amt_list` | varchar(500) | 支付金额列表 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
