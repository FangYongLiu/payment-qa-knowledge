---
id: tbl_counter_t_refund_ticket
object_type: Table
name: 出款退票记录表 (t_refund_ticket)
aliases: [t_refund_ticket, counter.t_refund_ticket]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: counter schema DDL
tags: [settlement, counter]
sensitivity: normal
related_services: []
---

# 出款退票记录表 (t_refund_ticket)

## 用途
物理表 `counter.t_refund_ticket`,主键 `ticket_id`。出款退票记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ticket_id` | bigint | 主键 |
| `request_no` | varchar(64) | 请求号 · 可空 |
| `fund_channel_code` | varchar(16) | 渠道编号 · 可空 |
| `biz_type` | varchar(4) | 业务类型 · 可空 |
| `inst_order_no` | varchar(32) | 机构订单号 · 可空 |
| `trade_time` | timestamp | 原交易时间 · 可空 |
| `voucher_no` | varchar(32) | 凭证编号 · 可空 |
| `product_code` | varchar(16) | 产品编码 · 可空 |
| `amount` | decimal(15, 2) | 交易金额 · 可空 |
| `currency` | varchar(3) | 币种 · 可空 |
| `status` | varchar(4) | 退票状态 I:初始化 S成功 F失败 · 可空 |
| `result_message` | varchar(256) | 响应信息 · 可空 |
| `memo` | varchar(256) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |
| `payment_order_no` | varchar(32) | 支付订单号 · 可空 |
| `bank_date` | timestamp | 银行退票时间 · 可空 |
| `bank_flow` | varchar(64) | 银行退票流水 · 可空 |
| `operator` | varchar(32) | 发起人 · 可空 |
| `file_name` | varchar(255) | 附件文件名称 · 可空 |
| `balance_status` | varchar(8) | 余额对账入账流水推送状态 · 可空 |
| `notify_status` | varchar(8) | 退票通知结果 · 可空 |
| `notify_message` | varchar(255) | 退票通知结果信息 · 可空 |
| `group_id` | int | 退票映射关系 · 可空 |
| `ticket_reason` | varchar(300) | 退票原因 · 可空 |
| `ticket_class` | varchar(100) | 退票分类 · 可空 |

## 主键 / 索引
- 主键:`ticket_id`
- `uk_requestNo`:request_no (UNIQUE)
- `idx_instOrderNo`:inst_order_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
