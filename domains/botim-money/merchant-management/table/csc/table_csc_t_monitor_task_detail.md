---
id: tbl_csc_t_monitor_task_detail
object_type: Table
name: 监控任务明细 (t_monitor_task_detail)
aliases: [t_monitor_task_detail, csc.t_monitor_task_detail]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: csc schema DDL
tags: [merchant-management, csc]
sensitivity: normal
related_services: []
---

# 监控任务明细 (t_monitor_task_detail)

## 用途
物理表 `csc.t_monitor_task_detail`,主键 `detail_id`。监控任务明细。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `detail_id` | bigint | 明细ID · 可空 |
| `task_id` | bigint | 任务ID |
| `key_value` | varchar(128) | 关键字段 · 可空 |
| `detail_content` | varchar(1000) | 明细内容 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`detail_id`
- `idx_key_value`:key_value
- `idx_task_id`:task_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
