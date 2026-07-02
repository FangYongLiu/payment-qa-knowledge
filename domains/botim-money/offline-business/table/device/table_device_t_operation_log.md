---
id: tbl_device_t_operation_log
object_type: Table
name: 操作日志 (t_operation_log)
aliases: [t_operation_log, device.t_operation_log]
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

# 操作日志 (t_operation_log)

## 用途
物理表 `device.t_operation_log`,主键 `id`。操作日志。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `merchant_mid` | varchar(32) | 商户mid |
| `device_id` | bigint | 待补 · 可空 |
| `operator` | varchar(200) | 员工姓名 |
| `category` | varchar(50) | 待补 |
| `operation` | varchar(50) | 操作 |
| `operation_time` | timestamp | 操作时间 |
| `detail` | varchar(200) | 备注 · 可空 |
| `created_time` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
