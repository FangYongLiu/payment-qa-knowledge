---
id: tbl_reconciliation_t_clear_flow
object_type: Table
name: 渠道清算流水详情 (t_clear_flow)
aliases: [t_clear_flow, reconciliation.t_clear_flow]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# 渠道清算流水详情 (t_clear_flow)

## 用途
物理表 `reconciliation.t_clear_flow`,主键 `parse_id`。渠道清算流水详情。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `parse_id` | varchar(32) | 待补 |
| `parse_batch_no` | varchar(64) | 对账单解析批次编号 · 可空 |
| `fund_channel_code` | varchar(32) | 渠道编号 · 可空 |
| `inst_order_no` | varchar(64) | 上送机构订单号 · 可空 |
| `inst_seq_no` | varchar(64) | 渠道返回订单号 · 可空 |
| `arn` | varchar(32) | ARN · 可空 |
| `file_seq_no` | varchar(32) | 文件序列号 · 可空 |
| `bill_date` | varchar(8) | 对账日期 · 可空 |
| `bill_flag` | varchar(4) | 对账状态 I:初始化 S:成功 M:多账(我方无渠道有) U:金额不等 · 可空 |
| `biz_type` | varchar(4) | 业务类型 · 可空 |
| `amount` | decimal(15, 2) | 交易金额 · 可空 |
| `currency` | varchar(3) | 货币 币种 · 可空 |
| `fee_amount` | decimal(15, 4) | 手续费 · 可空 |
| `fee_currency` | varchar(3) | 手续费币种 · 可空 |
| `settle_amount` | decimal(15, 4) | 结算金额 · 可空 |
| `settle_currency` | varchar(3) | 结算币种 · 可空 |
| `tran_date` | timestamp | 渠道交易时间 · 可空 |
| `status` | varchar(8) | 状态 · 可空 |
| `result_status` | varchar(64) | 渠道返回状态 · 可空 |
| `result_code` | varchar(64) | 渠道返回交易码 · 可空 |
| `result_msg` | varchar(256) | 渠道返回交易描述信息 · 可空 |
| `extension` | varchar(512) | 清算扩展信息 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 更新时间 |
| `channel_type` | varchar(4) | 渠道类型: SC 供应商渠道 , FC 资金渠道 · 可空 |
| `vat_amount` | decimal(15, 4) | 增值税 · 可空 |
| `vat_currency` | char(3) | 增值税币种 · 可空 |
| `settlement_date` | timestamp | 银行结算日期 · 可空 |
| `recon_extension` | varchar(512) | 对账扩展字段 · 可空 |

## 主键 / 索引
- 主键:`parse_id`
- `uk_inst_channel_biz`:inst_order_no, fund_channel_code, biz_type (UNIQUE)
- `idx_arn`:arn
- `idx_inst_seq_no`:inst_seq_no
- `idx_settlement_date_code`:settlement_date, fund_channel_code
- `inx_bill_date_code`:bill_date, fund_channel_code

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
