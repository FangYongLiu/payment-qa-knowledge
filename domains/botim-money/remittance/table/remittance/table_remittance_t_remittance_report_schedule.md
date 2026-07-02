---
id: tbl_remittance_t_remittance_report_schedule
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_remittance_report_schedule
subdomain: remittance
module: null
sensitivity: normal
name: 报表计划(t_remittance_report_schedule)
aliases:
- t_remittance_report_schedule
related_services:
- svc_remittance
related_scenarios: []
---
# 报表计划(t_remittance_report_schedule)

## 用途
报表计划。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键ID |
| `report_category` | varchar(32) |  | Report类型 |
| `report_type` | varchar(32) |  | Report类型 |
| `report_channel` | varchar(7) | NOT NULL | 报表所属渠道;MG |
| `trigger_cron` | varchar(20) | NOT NULL | cron表达式;用于计算下次执行时间 |
| `next_exec_time` | timestamp |  | 下次执行时间 |
| `last_exec_time` | timestamp |  | 最后一次执行时间 |
| `start_time_type` | char | NOT NULL | 其实时间类型;D：每日0点为开始时间，L：上一次执行时间为开始时间 |
| `file_name_rule` | varchar(100) |  | 文件名称规则 |
| `file_suffix` | char(4) |  | 文件类型;csv,xlsx |
| `file_path` | varchar(255) |  | 上传/下载路径;上传/下载的文件路径 |
| `max_retry_times` | int |  | 最大重试次数 |
| `delay_minutes` | int |  | 延迟执行时间(单位分钟) |
| `status` | char | NOT NULL | 状态;N:无效,Y:有效 |
| `extension` | varchar(255) |  | 扩展参数 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
