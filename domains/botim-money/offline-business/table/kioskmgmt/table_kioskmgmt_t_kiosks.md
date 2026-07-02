---
id: tbl_kioskmgmt_t_kiosks
object_type: Table
name: Ensures kiosk_id + vendor_name combination is unique (t_kiosks)
aliases: [t_kiosks, kioskmgmt.t_kiosks]
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: kioskmgmt schema DDL
tags: [offline-business, kioskmgmt]
sensitivity: normal
related_services: []
---

# Ensures kiosk_id + vendor_name combination is unique (t_kiosks)

## 用途
物理表 `kioskmgmt.t_kiosks`,主键 `entity_id`。Ensures kiosk_id + vendor_name combination is unique。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `entity_id` | varchar(36) | Internal system UUID for the entity |
| `kiosk_id` | varchar(100) | Business kiosk identifier |
| `payby_merchant_id` | varchar(30) | PayBy merchant identifier |
| `vendor_name` | varchar(20) | Vendor operating the kiosk |
| `location_name` | varchar(255) | Human-readable location name |
| `city` | varchar(100) | City where kiosk is located |
| `latitude` | decimal(10, 8) | GPS latitude coordinate |
| `longitude` | decimal(11, 8) | GPS longitude coordinate |
| `full_address` | varchar(500) | Complete physical address |
| `category` | varchar(30) | Business category type |
| `fees` | varchar(10) | Fee structure: Paid or Free |
| `open_time` | varchar(5) | Opening time in HH:MM format |
| `close_time` | varchar(5) | Closing time in HH:MM format |
| `image_references` | varchar(1000) | Array of image URLs/paths |
| `status` | varchar(20) | Current operational status |
| `created_at` | timestamp | Record creation timestamp |
| `updated_at` | timestamp | Last modification timestamp |
| `device_type` | varchar(10) | Device type |

## 主键 / 索引
- 主键:`entity_id`
- `idx_location_lat_lon`:latitude, longitude
- `idx_merchant`:payby_merchant_id
- `idx_vendor`:vendor_name

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
