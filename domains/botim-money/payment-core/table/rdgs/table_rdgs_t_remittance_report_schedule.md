---
id: tbl_rdgs_t_remittance_report_schedule
object_type: Table
name: 报表计划 (t_remittance_report_schedule)
aliases: [t_remittance_report_schedule, rdgs.t_remittance_report_schedule]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rdgs schema DDL
tags: [payment-core, rdgs]
sensitivity: normal
related_services: []
---

# 报表计划 (t_remittance_report_schedule)

## 用途
物理表 `rdgs.t_remittance_report_schedule`,主键 `id`。报表计划。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键ID · 可空 |
| `report_category` | varchar(32) | Report类型 · 可空 |
| `channel_code` | varchar(20) | report channel code;MG |
| `trigger_cron` | varchar(20) | cron表达式;用于计算下次执行时间 |
| `next_exec_time` | timestamp | 下次执行时间 · 可空 |
| `last_exec_time` | timestamp | 最后一次执行时间 · 可空 |
| `start_time_type` | char | 其实时间类型;D：每日0点为开始时间，L：上一次执行时间为开始时间 |
| `file_name_rule` | varchar(100) | 文件名称规则 · 可空 |
| `file_suffix` | char(4) | 文件类型;csv,xlsx · 可空 |
| `file_path` | varchar(255) | 上传/下载路径;上传/下载的文件路径 · 可空 |
| `max_retry_times` | int | 最大重试次数 · 可空 |
| `delay_minutes` | int | 延迟执行时间(单位分钟) · 可空 |
| `status` | char | 状态;N:无效,Y:有效 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `idx_create_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
