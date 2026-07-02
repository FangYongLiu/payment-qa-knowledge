---
id: tbl_outman_t_journey_result_detail
object_type: Table
name: Journey result detail (t_journey_result_detail)
aliases: [t_journey_result_detail, outman.t_journey_result_detail]
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

# Journey result detail (t_journey_result_detail)

## 用途
物理表 `outman.t_journey_result_detail`,主键 `id`。Journey result detail。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key |
| `journey_order_id` | bigint | Journey order id |
| `member_id` | varchar(20) | Member ID |
| `request_no` | varchar(80) | Request No |
| `channel_status` | varchar(64) | Original currentStatus returned by the channel · 可空 |
| `journey_info` | varchar(1150) | Raw capturedData/documentExtraction/selfieAnalysis/verificationLevel JSON · 可空 |
| `personal_info` | varchar(1024) | Personal Info · 可空 |
| `active_passport` | varchar(1024) | Active Passport · 可空 |
| `documents` | varchar(1024) | Digital documents (EID / signature / face photo ufs tag) · 可空 |
| `immigration_file` | varchar(1024) | Immigration file information · 可空 |
| `person_contact_details` | varchar(1024) | Personal contact details · 可空 |
| `residence_info` | varchar(1024) | Residence information · 可空 |
| `sponsor_contact_details` | varchar(1024) | Sponsor contact details · 可空 |
| `sponsor_details` | varchar(1024) | Sponsor details · 可空 |
| `active_visa` | varchar(1024) | Active Visa · 可空 |
| `travel_detail` | varchar(1024) | Travel record · 可空 |
| `source_association_details` | varchar(1024) | Source association details · 可空 |
| `valid` | char | Y: terminal-state record (canonical); N: intermediate or superseded · 可空 |
| `channel_resp_code` | varchar(64) | Channel response code of this get-result call · 可空 |
| `channel_resp_msg` | varchar(155) | Channel response message of this get-result call · 可空 |
| `errors` | varchar(1050) | JSON {journeyErrors:[...], customerErrors:[...]} from journey-detail / customer-detail · 可空 |
| `warnings` | varchar(1050) | JSON {journeyWarnings:[...], customerWarnings:[...]} · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`id`
- `j_order_id_idx`:journey_order_id
- `mid_idx`:member_id
- `req_no_idx`:request_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
