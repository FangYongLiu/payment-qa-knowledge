---
id: tbl_remittance_t_hold_report_record
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
- t_hold_report_record
subdomain: remittance
module: null
sensitivity: normal
name: Hold报表文件记录(t_hold_report_record)
aliases:
- t_hold_report_record
related_services:
- svc_remittance
related_scenarios: []
---
# Hold报表文件记录(t_hold_report_record)

## 用途
Hold报表文件记录。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `record_id` | bigint | PK / NOT NULL | 记录ID;8+9 |
| `channel_code` | varchar(7) | NOT NULL | 渠道CODE |
| `source_file_name` | varchar(100) | NOT NULL | 原文件名称 |
| `temp_path` | varchar(100) |  | 临时文件路径 |
| `file_tag` | varchar(64) |  | 上传ufs的文件tag |
| `analysis_times` | int |  | 文件解析次数;文件解析重试次数 |
| `total_count` | int |  | 解析记录总数 |
| `succ_count` | int |  | 解析成功记录数 |
| `offset` | int | NOT NULL | 偏移量;解析文件数据偏移量，初始0 |
| `version` | varchar(12) | NOT NULL | 文件版本;20230213 |
| `serial_no` | int | NOT NULL | 序号;用于标记当前是第几个文件 |
| `status` | char(2) | NOT NULL | 状态;DS,AP,AS,AF |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`record_id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
