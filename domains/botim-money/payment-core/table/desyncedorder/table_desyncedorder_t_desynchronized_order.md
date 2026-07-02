---
id: tbl_desyncedorder_t_desynchronized_order
object_type: Table
name: 未同步订单表 (t_desynchronized_order)
aliases: [t_desynchronized_order, desyncedorder.t_desynchronized_order]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: desyncedorder schema DDL
tags: [payment-core, desyncedorder]
sensitivity: normal
related_services: []
---

# 未同步订单表 (t_desynchronized_order)

## 用途
物理表 `desyncedorder.t_desynchronized_order`,主键 `id`。未同步订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 订单号 |
| `origin_global_id` | bigint | 原全局订单号 · 可空 |
| `merchant_order_no` | varchar(128) | 商户订单号 |
| `device_id` | varchar(32) | 设备ID |
| `partner_id` | varchar(32) | 发起方memberId |
| `client_order_type` | varchar(32) | 客户端订单类型 |
| `client_order_status` | varchar(200) | 客户端订单状态 |
| `currency_code` | varchar(8) |  币种 |
| `amount` | decimal(19, 4) | 金额 |
| `status` | varchar(32) | 订单状态 |
| `server_order_status` | varchar(32) | 服务端订单状态 · 可空 |
| `operator_id` | varchar(200) | 操作员ID · 可空 |
| `memo` | varchar(200) | memo · 可空 |
| `fail_code` | varchar(50) | 错误码 · 可空 |
| `fail_message` | varchar(200) | 错误描述 · 可空 |
| `origin_request_time` | timestamp(3) | 原请求时间 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `unity_result_code` | varchar(200) | 统一结果码 · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_ao_ct`:created_time
- `i_ao_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
