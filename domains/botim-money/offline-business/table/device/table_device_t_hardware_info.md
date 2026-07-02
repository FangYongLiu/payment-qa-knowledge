---
id: tbl_device_t_hardware_info
object_type: Table
name: 硬件信息 (t_hardware_info)
aliases: [t_hardware_info, device.t_hardware_info]
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

# 硬件信息 (t_hardware_info)

## 用途
物理表 `device.t_hardware_info`,主键 `id`。硬件信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 硬件id · 可空 |
| `sn_number` | varchar(64) | 硬件号 |
| `type` | varchar(32) | 类型 BOX 小白盒 SMART_POS 智能pos |
| `factory` | varchar(64) | 厂家 · 可空 |
| `created_time` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`id`
- `uk_sn_number_type`:sn_number, type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
