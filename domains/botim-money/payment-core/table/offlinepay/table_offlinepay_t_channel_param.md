---
id: tbl_offlinepay_t_channel_param
object_type: Table
name: Channel Param (t_channel_param)
aliases: [t_channel_param, offlinepay.t_channel_param]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: offlinepay schema DDL
tags: [payment-core, offlinepay]
sensitivity: normal
related_services: []
---

# Channel Param (t_channel_param)

## 用途
物理表 `offlinepay.t_channel_param`,主键 `global_id`。Channel Param。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | global_id |
| `card_auth_no` | varchar(64) | card_authorization_no · 可空 |
| `card_transaction_no` | varchar(64) | card_transaction_no · 可空 |
| `iso8583_resp_code` | varchar(64) | iso8583_response_code · 可空 |
| `ticket_id` | varchar(32) | ticket_id · 可空 |
| `created_time` | timestamp(3) | created_time |
| `last_updated_time` | timestamp(3) | last_updated_time |
| `data_version` | bigint | data_version |
| `tran_currency_code` | varchar(64) | tran currency code · 可空 |

## 主键 / 索引
- 主键:`global_id`
- `i_cp_ct`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
