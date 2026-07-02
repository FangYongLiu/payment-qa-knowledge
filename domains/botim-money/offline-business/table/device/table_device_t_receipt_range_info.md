---
id: tbl_device_t_receipt_range_info
object_type: Table
name: 收据号段信息表 (t_receipt_range_info)
aliases: [t_receipt_range_info, device.t_receipt_range_info]
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

# 收据号段信息表 (t_receipt_range_info)

## 用途
物理表 `device.t_receipt_range_info`,主键 `id`。收据号段信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `identity_id` | varchar(32) | 标识id |
| `identity_type` | varchar(32) | 标识类型 |
| `receipt_no` | bigint | 收据号 |
| `created_time` | timestamp | 创建时间 |
| `last_updated_time` | timestamp | 最后修改时间 |
| `data_version` | bigint | 版本号 |

## 主键 / 索引
- 主键:`id`
- `uk_receipt`:identity_id, identity_type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
