---
id: tbl_npss_t_order_ext
object_type: Table
name: 订单扩展表 (t_order_ext)
aliases: [t_order_ext, npss.t_order_ext]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: npss schema DDL
tags: [payment-core, npss]
sensitivity: normal
related_services: []
---

# 订单扩展表 (t_order_ext)

## 用途
物理表 `npss.t_order_ext`,主键 `ext_id`。订单扩展表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ext_id` | bigint | 扩展id |
| `ext_type` | varchar(10) | 扩展类型 |
| `related_id` | bigint | 关联id |
| `device_version` | varchar(32) | 设备版本 · 可空 |
| `device_model` | varchar(32) | 设备型号 · 可空 |
| `ip_address` | varchar(32) | ip地址 · 可空 |
| `consent_id` | varchar(64) | 同意id · 可空 |
| `payment_id` | bigint(32) | 银行订单id · 可空 |
| `os_version` | varchar(32) | payby app版本号 · 可空 |
| `clr_sys_no` | varchar(32) | 清算订单号 · 可空 |

## 主键 / 索引
- 主键:`ext_id`
- `uk_ext_id`:related_id, ext_type (UNIQUE)
- `idx_order_ext_payment_id`:payment_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
