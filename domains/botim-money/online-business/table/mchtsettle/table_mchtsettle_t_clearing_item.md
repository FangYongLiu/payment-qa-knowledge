---
id: tbl_mchtsettle_t_clearing_item
object_type: Table
name: 清算条目表 (t_clearing_item)
aliases: [t_clearing_item, mchtsettle.t_clearing_item]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mchtsettle schema DDL
tags: [online-business, 商户结算, mchtsettle]
sensitivity: normal
related_services: [svc_merchant_settlement]
---

# 清算条目表 (t_clearing_item)

## 用途
物理表 `mchtsettle.t_clearing_item`,主键 `id`。clearing_item。属商户结算服务 [[svc_merchant_settlement]]。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:[[svc_merchant_settlement]](= `related_services`)。
- **谁读写它**:结算链路的服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `batch_id` | bigint | batch id |
| `product_code` | varchar(200) | product code |
| `merchant_mid` | varchar(50) | merchant mid · 可空 |
| `acquire_data` | varchar(200) | acquire data · 可空 |
| `area` | varchar(20) | area · 可空 |
| `arn` | varchar(200) | arn · 可空 |
| `auth_code` | varchar(200) | auth code · 可空 |
| `bank_net_mid` | varchar(200) | bank net merchant_id · 可空 |
| `card_num` | varchar(32) | card num · 可空 |
| `card_type` | varchar(16) | card type · 可空 |
| `sales_currency` | char(3) | sales currency · 可空 |
| `sales_amount` | decimal(19,4) | sales amount · 可空 |
| `status` | varchar(16) | status · 可空 |
| `terminal_id` | varchar(200) | terminal id · 可空 |
| `transaction_type` | varchar(20) | transaction type · 可空 |
| `transaction_time` | timestamp(3) | transaction time · 可空 |
| `bank_account` | varchar(200) | bank account · 可空 |
| `banknet_mid` | varchar(200) | banknet mid · 可空 |
| `bat` | varchar(200) | bat · 可空 |
| `card_usage` | varchar(200) | card usage · 可空 |
| `chain_id` | varchar(200) | chain id · 可空 |
| `commission_amount` | decimal(19,4) | commission amount · 可空 |
| `commission_currency` | char(3) | commission currency · 可空 |
| `disc_type` | varchar(200) | disc type · 可空 |
| `driver_id` | varchar(200) | driver id · 可空 |
| `inter_change` | varchar(200) | inter change · 可空 |
| `location` | varchar(200) | location · 可空 |
| `master_chain_id` | varchar(200) | master chain id · 可空 |
| `merchant_name` | varchar(200) | merchant name · 可空 |
| `net_amount` | decimal(19,4) | net amount · 可空 |
| `net_currency` | char(3) | net currency · 可空 |
| `order_reference` | varchar(200) | order reference · 可空 |
| `pwcb_cash_back` | varchar(200) | pwcb cash back · 可空 |
| `reference_no` | varchar(200) | reference no · 可空 |
| `sequence_number` | varchar(200) | sequence number · 可空 |
| `srl_no` | varchar(200) | srl no · 可空 |
| `tag_id` | varchar(200) | tag id · 可空 |
| `telephone` | varchar(200) | telephone · 可空 |
| `tip_amount` | decimal(19,4) | tip amount · 可空 |
| `tip_currency` | char(3) | tip currency · 可空 |
| `token_tran_id` | varchar(200) | token tran_id · 可空 |
| `trans_source` | varchar(200) | trans source · 可空 |
| `ty` | varchar(200) | ty · 可空 |
| `vat_amount` | decimal | vat amount · 可空 |
| `vat_currency` | char(3) | vat currency · 可空 |
| `created_time` | timestamp(3) | created time |
| `last_updated_time` | timestamp(3) | last updated time |
| `data_version` | bigint | data version |
| `city` | varchar(150) | submerchant city · 可空 |
| `country` | varchar(100) | submerchant country · 可空 |
| `pay_facilitator_id` | varchar(150) | facilitator id · 可空 |
| `sub_merchant_id` | varchar(150) | submerchant id · 可空 |
| `trans_mcc` | varchar(100) | submerchant sic mcc · 可空 |
| `payfac_sub_merchant` | varchar(150) | payfacs subMerchant · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_ref_tran_type`:reference_no, transaction_type (UNIQUE)
- `i_batch_id_status`:batch_id, status
- `i_ci_arn`:arn
- `i_ci_ct`:created_time

## 校验点(QA 关注)
- **时间字段**:`created_time`=入库、`last_updated_time`=最后更新;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发场景校验版本递增。
- **金额精度**:decimal 金额比较用容差(< 0.01);amount 与对应 currency 成对、需一致。
- **批次维度**:`batch_id` 关联清算批次 t_clearing_batch。
- **商户维度**:`merchant_mid` 为商户号,按商户聚合/对账。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
