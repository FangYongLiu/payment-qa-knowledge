---
id: tbl_device_t_device_delivery_history
object_type: Table
name: t_device_delivery_history (t_device_delivery_history)
aliases: [t_device_delivery_history, device.t_device_delivery_history]
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: device schema DDL
tags: [offline-business, device]
sensitivity: normal
related_services: []
---

# t_device_delivery_history (t_device_delivery_history)

## 用途
物理表 `device.t_device_delivery_history`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `device_id` | bigint | Device id |
| `created_time` | timestamp | Record creation time |
| `status` | varchar(20) | Delivery status |
| `remark` | varchar(500) | Additional remarks · 可空 |
| `installed_by` | varchar(50) | Staff name who installed the device · 可空 |
| `installation_date` | timestamp | Date when device was installed · 可空 |
| `site_photos` | varchar(255) | Photos taken at installation site · 可空 |
| `merchant_ack` | varchar(100) | Merchant acknowledgement documents · 可空 |
| `other_docs` | varchar(512) | Other related documents · 可空 |
| `data_version` | bigint | Data version for concurrency control |
| `created_by` | varchar(100) | User who created the record · 可空 |
| `operator_id` | bigint | Operator ID who performed the action |
| `operator_name` | varchar(50) | Name of the operator |
| `last_updated_time` | timestamp | Last update timestamp · 可空 |
| `updated_by` | varchar(100) | User who last updated the record · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_created_time`:created_time
- `idx_device_id`:device_id
- `idx_installed_by`:installed_by

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
