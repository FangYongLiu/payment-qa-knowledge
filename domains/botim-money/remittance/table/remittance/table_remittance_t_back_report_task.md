---
id: tbl_remittance_t_back_report_task
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
- t_back_report_task
subdomain: remittance
module: null
sensitivity: normal
name: 回盘任务(t_back_report_task)
aliases:
- t_back_report_task
related_services:
- svc_remittance
related_scenarios: []
---
# 回盘任务(t_back_report_task)

## 用途
回盘任务。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `task_id` | bigint | PK / NOT NULL | TASK ID;8+9 |
| `channel_code` | varchar(7) | NOT NULL | 渠道CODE |
| `biz_type` | varchar(12) |  | Sender;Receiver |
| `file_name` | varchar(128) |  | 文件名称 |
| `upload_channel_path` | varchar(255) |  | 上传渠道路径;上传sftp的文件路径+文件名 |
| `upload_channel_times` | int |  | 上传渠道次数 |
| `file_tag` | varchar(64) |  | 上传ufs的文件tag |
| `file_suffix` | char(4) | NOT NULL | 文件类型；csv;xlsx |
| `version` | varchar(12) | NOT NULL | 文件版本;20230213 |
| `serial_no` | int | NOT NULL | 序列号;用于标记当前是第几个文件 |
| `status` | char(3) | NOT NULL | 状态;I,W,CE,CS,UE,,US |
| `start_time` | timestamp | NOT NULL | 开始时间;捞取数据的开始时间-包含 |
| `end_time` | timestamp | NOT NULL | 结束时间;捞取数据的结束时间-不包含 |
| `total_count` | int |  | 回盘记录总数 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`task_id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
