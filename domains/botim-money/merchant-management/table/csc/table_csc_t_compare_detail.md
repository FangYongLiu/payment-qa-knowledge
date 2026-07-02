---
id: tbl_csc_t_compare_detail
object_type: Table
name: 对账明细 (t_compare_detail)
aliases: [t_compare_detail, csc.t_compare_detail]
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

# 对账明细 (t_compare_detail)

## 用途
物理表 `csc.t_compare_detail`,主键 `detail_id`。对账明细。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `detail_id` | bigint | 明细ID · 可空 |
| `task_id` | bigint | 任务ID |
| `relate_identity` | varchar(128) | 关联标志 |
| `src_data` | varchar(1000) | 源数据 · 可空 |
| `target_data` | varchar(1000) | 目标数据 · 可空 |
| `compare_status` | char | 比对状态：L=少数据，M=不一致 |
| `compensate_flag` | char | 补单标志：W=等待补单，S=补单成功，F=补单失败，E=补单异常 · 可空 |
| `error_message` | varchar(128) | 错误信息 · 可空 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`detail_id`
- `idx_relate_identity`:relate_identity
- `idx_task_id`:task_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
