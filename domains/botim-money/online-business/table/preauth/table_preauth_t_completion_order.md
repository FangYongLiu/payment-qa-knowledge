---
id: tbl_preauth_t_completion_order
object_type: Table
name: 完成订单 (t_completion_order)
aliases: [t_completion_order, preauth.t_completion_order]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: preauth schema DDL
tags: [online-business, preauth]
sensitivity: normal
related_services: []
---

# 完成订单 (t_completion_order)

## 用途
物理表 `preauth.t_completion_order`,主键 `global_id`。完成订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局号 |
| `request_no` | varchar(200) | 等同于requestIdentity.requestNo.查询方便 |
| `mis_order_no` | varchar(200) | 商户mis系统订单号 · 可空 |
| `origin_global_id` | bigint | 原始订单号 |
| `retransmission` | int | 重发计数 |
| `device_id` | varchar(200) | 发起方设备id |
| `partner_id` | varchar(32) | 发起方memberId |
| `currency_code` | varchar(50) | 预授权完成币种 |
| `amount` | decimal(19, 4) | 预授权完成金额 |
| `acquire_order_id` | bigint | 收单订单id · 可空 |
| `res_payload_token` | varchar(32) | 返回ues_token · 可空 |
| `current_cmd_id` | bigint | 当前cmdid · 可空 |
| `status` | varchar(50) | 收单状态 |
| `fail_code` | varchar(50) | 错误码 · 可空 |
| `fail_message` | varchar(200) | 错误描述 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `unity_result_code` | varchar(200) | 统一结果码 · 可空 |

## 主键 / 索引
- 主键:`global_id`
- `i_co_ct`:created_time
- `i_co_lut`:last_updated_time
- `i_co_ogi`:origin_global_id
- `i_co_rn`:request_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
