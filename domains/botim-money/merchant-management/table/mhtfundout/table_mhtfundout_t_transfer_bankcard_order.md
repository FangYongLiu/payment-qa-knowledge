---
id: tbl_mhtfundout_t_transfer_bankcard_order
object_type: Table
name: transferBankcardOrder (t_transfer_bankcard_order)
aliases: [t_transfer_bankcard_order, mhtfundout.t_transfer_bankcard_order]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mhtfundout schema DDL
tags: [merchant-management, mhtfundout]
sensitivity: normal
related_services: []
---

# transferBankcardOrder (t_transfer_bankcard_order)

## 用途
物理表 `mhtfundout.t_transfer_bankcard_order`,主键 `global_id`。transferBankcardOrder。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | global_id |
| `beneficiary_id` | bigint | beneficiary_id |
| `request_no` | varchar(32) | request_no |
| `partner_id` | varchar(32) | partner_id |
| `currency` | char(3) | currency |
| `amount` | decimal(19, 2) | amount |
| `status` | varchar(16) | status |
| `creator_mid` | varchar(32) | creator_mid · 可空 |
| `bank_reference` | varchar(128) | bank_reference · 可空 |
| `product_code` | varchar(16) | productCode |
| `notify_url` | varchar(255) | notify_url · 可空 |
| `memo` | varchar(128) | memo · 可空 |
| `fail_code` | varchar(50) | fail_code · 可空 |
| `fail_message` | varchar(200) | fail_message · 可空 |
| `unity_result_code` | varchar(64) | unity_result_code · 可空 |
| `created_time` | timestamp(3) | created_time |
| `last_updated_time` | timestamp(3) | last_updated_time |
| `data_version` | bigint | data_version |
| `sender_type` | varchar(16) | sender type · 可空 |
| `sender_info_id` | bigint | sender_info_id · 可空 |

## 主键 / 索引
- 主键:`global_id`
- `i_tbo_ct`:created_time
- `i_tbo_lut`:last_updated_time
- `i_tbo_pi`:partner_id
- `i_tbo_rn`:request_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
