---
id: tbl_counter_t_charge_back_order
object_type: Table
name: Charge Back 抗辩订单 (t_charge_back_order)
aliases: [t_charge_back_order, counter.t_charge_back_order]
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

# Charge Back 抗辩订单 (t_charge_back_order)

## 用途
物理表 `counter.t_charge_back_order`,主键 `flow_id`。Charge Back 抗辩订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `flow_id` | bigint(17) | 主键 |
| `fund_channel_code` | varchar(32) | 渠道编号 |
| `biz_type` | varchar(4) | 业务类型 |
| `inst_order_no` | varchar(64) | 机构订单号 |
| `payment_order_no` | varchar(64) | 支付订单号 |
| `amount` | decimal(15, 2) | 交易金额 · 可空 |
| `currency` | varchar(3) | 币种 · 可空 |
| `message` | varchar(255) | 响应信息 · 可空 |
| `status` | varchar(16) | 状态 · 可空 |
| `accounting_status` | varchar(8) | 记账状态 · 可空 |
| `dis_voucher_no` | varchar(64) | 抗辩订单申请记账凭证号 · 可空 |
| `rec_voucher_no` | varchar(64) | 抗辩扣款凭证号 · 可空 |
| `basic_account` | varchar(64) | 准备金Basic账户 · 可空 |
| `pending_account` | varchar(64) | 准备金 拒付待确认账户 · 可空 |
| `oss_path` | varchar(128) | OSS Path · 可空 |
| `updator` | varchar(64) | 更新人 · 可空 |
| `creator` | varchar(64) | 创建人 · 可空 |
| `extension` | varchar(512) | 扩展信息 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |
| `basic_member_id` | varchar(32) | 准备金Basic 会员号 · 可空 |
| `pending_member_id` | varchar(32) | 准备金 拒付待确认 会员号 · 可空 |
| `chargeback_amount` | decimal(15, 2) | 拒付金额 · 可空 |
| `loss_amount` | decimal(15, 2) | 赔付金额 · 可空 |

## 主键 / 索引
- 主键:`flow_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
