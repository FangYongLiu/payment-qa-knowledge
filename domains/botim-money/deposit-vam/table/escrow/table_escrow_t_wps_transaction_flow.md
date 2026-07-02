---
id: tbl_escrow_t_wps_transaction_flow
object_type: Table
name: 工资流水号唯一索引 (t_wps_transaction_flow)
aliases: [t_wps_transaction_flow, escrow.t_wps_transaction_flow]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: escrow schema DDL
tags: [deposit-vam, escrow]
sensitivity: normal
related_services: []
---

# 工资流水号唯一索引 (t_wps_transaction_flow)

## 用途
物理表 `escrow.t_wps_transaction_flow`,主键 `wps_transaction_id`。工资流水号唯一索引。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `wps_transaction_id` | bigint(19) | 流水ID |
| `card_id` | varchar(32) | 卡id |
| `card_no` | varchar(32) | 卡号 |
| `member_id` | varchar(32) | 会员编号 |
| `reference_no` | varchar(32) | wps编号 |
| `available_amount` | decimal(19, 4) | 可用金额 · 可空 |
| `current_amount` | decimal(19, 4) | 剩余金额 · 可空 |
| `transaction_amount` | decimal(19, 4) | 交易金额 · 可空 |
| `currency` | varchar(8) | 币种 |
| `transaction_type` | varchar(16) | 流水交易类型 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modify` | timestamp | 更新时间 · 可空 |
| `inner_trans_status` | varchar(8) | 内部交易状态，S-成功, R-重试,P-处理中，F-失败 · 可空 |
| `inner_trans_code` | varchar(16) | 内部交易响应码 · 可空 |
| `inner_trans_message` | varchar(128) | 内部交易响应描述 · 可空 |
| `con_status` | varchar(8) | 对账状态 · 可空 |
| `inner_trans_order` | varchar(64) | 内部订单号 · 可空 |
| `memo` | varchar(1024) | 拓展字段 · 可空 |
| `gmt_trans_finish` | timestamp | 交易成功时间 · 可空 |

## 主键 / 索引
- 主键:`wps_transaction_id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
