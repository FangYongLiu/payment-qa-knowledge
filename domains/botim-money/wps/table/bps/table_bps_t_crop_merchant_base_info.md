---
id: tbl_bps_t_crop_merchant_base_info
object_type: Table
name: corporate merchant base info (t_crop_merchant_base_info)
aliases: [t_crop_merchant_base_info, bps.t_crop_merchant_base_info]
domain: wps
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: bps schema DDL
tags: [wps, bps]
sensitivity: normal
related_services: []
---

# corporate merchant base info (t_crop_merchant_base_info)

## 用途
物理表 `bps.t_crop_merchant_base_info`,主键 `id`。corporate merchant base info。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | ulid |
| `merchant_id` | varchar(32) | merchant id |
| `customer` | varchar(100) | customer name |
| `address` | varchar(255) | address |
| `trn` | varchar(64) | trn |
| `create_at` | timestamp | create time · 可空 |
| `update_at` | timestamp | update time · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
