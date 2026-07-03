---
id: tbl_casheatm_t_cash_delivery_order
object_type: Table
name: cash delivery  订单 (t_cash_delivery_order)
aliases: [t_cash_delivery_order, casheatm.t_cash_delivery_order]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: casheatm schema DDL
tags: [online-business, casheatm]
sensitivity: normal
related_services: [svc_cash_eatm]
---

# cash delivery  订单 (t_cash_delivery_order)

## 用途
物理表 `casheatm.t_cash_delivery_order`,主键 `global_id`。cash delivery  订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局号 |
| `currency_code` | varchar(50) | 收单币种代码 |
| `amount` | decimal(19, 4) | cash_out金额 |
| `fee_amount` | decimal(19, 4) | 用户费用金额 · 可空 |
| `device_id` | bigint | 设备id |
| `merchant_mid` | varchar(200) | 收款人mid |
| `customer_mid` | varchar(200) | 付款人mid |
| `pay_scene_code` | varchar(32) | 待补 · 可空 |
| `status` | varchar(200) | 收单状态 |
| `unity_result_code` | varchar(200) | 统一结果码 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `rider_id` | bigint | 骑手id |
| `code` | varchar(200) | 密码 |

## 主键 / 索引
- 主键:`global_id`
- `i_cdo_ct`:created_time
- `i_cdo_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
