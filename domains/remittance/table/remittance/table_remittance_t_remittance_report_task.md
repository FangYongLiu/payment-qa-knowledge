---
id: tbl_remittance_t_remittance_report_task
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
- t_remittance_report_task
subdomain: remittance
module: null
sensitivity: normal
name: t_remittance_report_task
aliases:
- t_remittance_report_task
related_services:
- svc_remittance
related_scenarios: []
---
# t_remittance_report_task

## 用途
待补。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键id |
| `report_channel` | varchar(7) |  | 报表所属渠道;MG |
| `report_category` | varchar(32) | NOT NULL | 报表类别 |
| `upload_path` | varchar(255) |  | 上传/下载路径;上传/下载的文件路径 |
| `file_name` | varchar(64) |  | 文件名称 |
| `file_tag` | varchar(64) |  | 上传ufs的文件tag |
| `file_suffix` | char(4) |  | 文件类型；csv;xlsx |
| `version` | varchar(12) | NOT NULL | 文件版本;202302130000 |
| `status` | char | NOT NULL | 状态I，W，E，S |
| `start_time` | timestamp | NOT NULL | 开始时间;捞取数据的开始时间-包含 |
| `end_time` | timestamp | NOT NULL | 结束时间;捞取数据的结束时间-不包含 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |
| `remaining_retry_times` | int |  | 剩余异常重试次数 |
| `total_count` | int(12) |  | 总条数 |
| `total_amount` | decimal(19,4) |  | 汇款总金额 |
| `extension` | varchar(255) |  | 扩展参数 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
