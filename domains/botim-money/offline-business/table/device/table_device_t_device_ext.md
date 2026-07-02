---
id: tbl_device_t_device_ext
object_type: Table
name: 设备扩展表 (t_device_ext)
aliases: [t_device_ext, device.t_device_ext]
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

# 设备扩展表 (t_device_ext)

## 用途
物理表 `device.t_device_ext`,主键 `device_id, pkey`。设备扩展表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `device_id` | bigint | 明细ID |
| `pkey` | varchar(200) | 参数键 |
| `value` | varchar(500) | 参数值 |

## 主键 / 索引
- 主键:`device_id, pkey`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
