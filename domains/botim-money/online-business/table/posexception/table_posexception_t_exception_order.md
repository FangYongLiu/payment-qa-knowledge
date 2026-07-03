---
id: tbl_posexception_t_exception_order
object_type: Table
name: 异常订单表 (t_exception_order)
aliases: [t_exception_order, posexception.t_exception_order]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: posexception schema DDL
tags: [online-business, posexception]
sensitivity: normal
related_services: [svc_pos_exception_processor]
---

# 异常订单表 (t_exception_order)

## 用途
物理表 `posexception.t_exception_order`,主键 `id`。异常订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 订单号 |
| `device_id` | varchar(32) | 设备ID |
| `request_no` | varchar(128) | 商户订单号 |
| `partner_id` | varchar(32) | 发起方memberId |
| `transaction_type` | varchar(32) | transactionType |
| `reversal` | varchar(32) | reversal |
| `execution_result` | varchar(32) | executionResult |
| `channel_code` | varchar(32) | 渠道代码 |
| `status` | varchar(32) | 订单状态 |
| `last_operator_mid` | varchar(64) | 操作员ID · 可空 |
| `last_memo` | varchar(200) | lastMemo · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `uk_di_rn`:device_id, request_no (UNIQUE)
- `i_ao_ct`:created_time
- `i_ao_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
