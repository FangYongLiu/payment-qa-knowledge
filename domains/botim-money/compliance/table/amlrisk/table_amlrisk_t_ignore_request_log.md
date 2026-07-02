---
id: tbl_amlrisk_t_ignore_request_log
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: amlrisk schema DDL
tags:
- amlrisk
- t_ignore_request_log
subdomain: amlrisk
module: null
sensitivity: normal
name: Focal 忽略请求日志表 (t_ignore_request_log)
aliases:
- t_ignore_request_log
- amlrisk.t_ignore_request_log
related_services: []
---

# Focal 忽略请求日志表 (t_ignore_request_log)

## 用途
物理表 `amlrisk.t_ignore_request_log`,主键 `id`。Focal ignore outbound request log。属 AML 风控库 `amlrisk`(向 Focal 发送 ignore 出站请求的日志)。业务语义细节**待补**。

## 关联关系
- **所属服务**:待补(compliance 域 AML 风控服务)。
- **谁读写它**:AML/风控链路服务(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `personal_id` | bigint | personalId · 可空 |
| `eid` | varchar(20) | eid · 可空 |
| `customer_reference_id` | varchar(32) | customerReferenceId |
| `handler_type` | varchar(32) | handlerType |
| `focal_code` | varchar(32) | focalCode · 可空 |
| `focal_msg` | varchar(128) | focalMsg · 可空 |
| `success` | char | success · 可空 |
| `created_time` | timestamp | createdTime · 可空 |
| `updated_time` | timestamp | updatedTime · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_ignore_log_created_time`:created_time
- `idx_ignore_log_customer_ref`:customer_reference_id
- `idx_ignore_log_eid`:eid
- `idx_ignore_log_personal_id`:personal_id
- `idx_ignore_log_updated_time`:updated_time

## 校验点(QA 关注)
- **时间字段**:`created_time`/`updated_time`;按时间过滤走对应索引。
- **关联维度**:`personal_id`/`eid`/`customer_reference_id` 关联个人扫描信息与 Focal 请求。
- **success**:请求成功标志;失败记录用于排查 Focal 出站 ignore 未生效。
- 更细规则**待补**(需结合代码或业务文档)。
