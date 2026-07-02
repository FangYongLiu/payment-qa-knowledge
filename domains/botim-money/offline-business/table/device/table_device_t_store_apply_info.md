---
id: tbl_device_t_store_apply_info
object_type: Table
name: 门店申请信息 (t_store_apply_info)
aliases: [t_store_apply_info, device.t_store_apply_info]
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

# 门店申请信息 (t_store_apply_info)

## 用途
物理表 `device.t_store_apply_info`,主键 `id`。门店申请信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `name` | varchar(64) | 门店名称 |
| `location` | varchar(64) | 门店地址 |
| `store_entrance_photo_path` | varchar(200) | 门头照路径 |
| `cash_desk_photo_path` | varchar(200) | 收银台照路径 |
| `created_time` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
