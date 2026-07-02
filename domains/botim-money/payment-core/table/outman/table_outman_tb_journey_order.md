---
id: tbl_outman_tb_journey_order
object_type: Table
name: journey verification table (tb_journey_order)
aliases: [tb_journey_order, outman.tb_journey_order]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: outman schema DDL
tags: [payment-core, outman]
sensitivity: normal
related_services: []
---

# journey verification table (tb_journey_order)

## 用途
物理表 `outman.tb_journey_order`,主键 `journey_order_id`。journey verification table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `journey_order_id` | bigint | Primary key ID; 8+9 |
| `request_no` | varchar(32) | Request number; unique request identifier |
| `member_id` | varchar(20) | Member ID |
| `channel_code` | varchar(32) | Channel code |
| `customer_id` | varchar(64) | Channel customer ID · 可空 |
| `flow_id` | varchar(64) | KYC flow ID · 可空 |
| `journey_id` | varchar(64) | Channel id; token obtained from the channel · 可空 |
| `journey_url` | varchar(200) | URL; video URL returned by the liveness channel · 可空 |
| `journey_type` | varchar(6) | FKF:Full Kyc Flow, BA:Body Auth · 可空 |
| `status` | varchar(12) | Status; INIT, PROCESS, FAIL, SUCCESS, CLOSED |
| `step` | varchar(12) | Step; FKF, KRLF |
| `retake_channel_code` | varchar(32) | Channel code · 可空 |
| `retake_flow_id` | varchar(64) | Retake flow ID · 可空 |
| `retake_journey_id` | varchar(32) | Channel id; token obtained from the channel · 可空 |
| `retake_journey_url` | varchar(200) | URL; video URL returned by the liveness channel · 可空 |
| `category` | varchar(15) | Category: EID/PASSPORT · 可空 |
| `next_query_time` | timestamp | Next Query Time · 可空 |
| `query_retry_times` | tinyint(2) | Query Retry Times, eg: 1 · 可空 |
| `extension` | varchar(250) | Extended data · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `gmt_create` | timestamp | Creation time |
| `gmt_modified` | timestamp | Update time |

## 主键 / 索引
- 主键:`journey_order_id`
- `idx_query_time`:next_query_time
- `mid_idx`:member_id
- `req_no_idx`:request_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
