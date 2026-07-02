---
id: tbl_cregister_t_register_order
object_type: Table
name: Registration Order (t_register_order)
aliases: [t_register_order, cregister.t_register_order]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cregister schema DDL
tags: [merchant-management, cregister]
sensitivity: normal
related_services: []
---

# Registration Order (t_register_order)

## 用途
物理表 `cregister.t_register_order`,主键 `register_id`。Registration Order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `register_id` | bigint | Order ID; 8+9 |
| `request_no` | varchar(64) | Unique Request Number |
| `merchant_id` | varchar(32) | Merchant Number |
| `inst_order_no` | varchar(32) | Institution Order Number |
| `inst_code` | varchar(24) | Institution Code |
| `fund_channel_code` | varchar(24) | Channel Code |
| `fund_provider_code` | varchar(24) | Channel Provider |
| `register_type` | varchar(12) | Registration Type; MERCHANT: Merchant, STORE: Store, DEVICE: Device |
| `request_type` | varchar(12) | Request Type; MCR: MERCHANT_REGISTER |
| `api_type` | varchar(12) | API Type |
| `flag` | char | Flag Status; Used for temporarily updating the flag during order query operations |
| `retry_times` | int | Query Times; Initially 0 |
| `gmt_next_retry` | timestamp | Next Retry Query Result Time · 可空 |
| `gmt_booking_time` | timestamp | Scheduled Registration Time · 可空 |
| `register_info` | varchar(1200) | Registration Information; JSON Format · 可空 |
| `extension` | varchar(1024) | Extension Information; JSON Format · 可空 |
| `archive_batch_id` | bigint | Batch Number; Initial value for batch reported orders is 0 · 可空 |
| `communicate_status` | varchar(1) | Channel Communication Status for Single Orders: A (Waiting for Instruction Send), I (Sending), S (Instruction Sent), R (Data Returned), F (Instruction Send Failed) |
| `communicate_type` | varchar(12) | Communication Type; BATCH, SINGLE |
| `inner_id` | varchar(64) | Biz inner ID · 可空 |
| `channel_issue_id` | varchar(64) | Channel Assigned ID; Can be obtained after channel registration · 可空 |
| `merchant_channel_id` | varchar(64) | Merchant Channel Id · 可空 |
| `store_channel_id` | varchar(64) | Store Channel Id · 可空 |
| `device_channel_id` | varchar(64) | Device Channel Id · 可空 |
| `register_result` | varchar(355) | Registration Result; Channel Registration Result MAP - JSON Format · 可空 |
| `status` | char | Status I: Processing, S: Success, F: Fail |
| `channel_return_msg` | varchar(255) | Channel return msg · 可空 |
| `is_notify` | char | Notification Status; Y/N |
| `memo` | varchar(100) | Remark · 可空 |
| `gmt_create` | timestamp | Creation Time |
| `gmt_modified` | timestamp | Update Time |

## 主键 / 索引
- 主键:`register_id`
- `idx_batch_id`:archive_batch_id
- `idx_channel_issue_id`:channel_issue_id
- `idx_create`:gmt_create
- `idx_next_retry_time`:gmt_next_retry
- `idx_order_no`:inst_order_no
- `idx_req_no`:request_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
