---
id: tbl_device_t_terminal_trace_no
object_type: Table
name: 设备跟踪号 (t_terminal_trace_no)
aliases: [t_terminal_trace_no, device.t_terminal_trace_no]
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

# 设备跟踪号 (t_terminal_trace_no)

## 用途
物理表 `device.t_terminal_trace_no`,主键 `id`。设备跟踪号。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | group id · 可空 |
| `terminal_id` | varchar(32) | 终端id |
| `channel_code` | varchar(32) | 渠道编码 |
| `last_trace_no` | int | POS跟踪号 |
| `backend_trace_no` | int | 后端跟踪号 |
| `created_time` | timestamp | 创建时间 |
| `last_updated_time` | timestamp | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `UID_TID_CCODE`:terminal_id, channel_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
