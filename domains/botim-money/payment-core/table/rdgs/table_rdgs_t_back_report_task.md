---
id: tbl_rdgs_t_back_report_task
object_type: Table
name: 回盘任务 (t_back_report_task)
aliases: [t_back_report_task, rdgs.t_back_report_task]
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

# 回盘任务 (t_back_report_task)

## 用途
物理表 `rdgs.t_back_report_task`,主键 `task_id`。回盘任务。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `task_id` | bigint | TASK ID;8+9 |
| `channel_code` | varchar(7) | 渠道CODE |
| `biz_type` | varchar(12) | Sender;Receiver · 可空 |
| `file_name` | varchar(128) | 文件名称 · 可空 |
| `upload_channel_path` | varchar(255) | 上传渠道路径;上传sftp的文件路径+文件名 · 可空 |
| `upload_channel_times` | int | 上传渠道次数 · 可空 |
| `file_tag` | varchar(64) | 上传ufs的文件tag · 可空 |
| `file_suffix` | char(4) | 文件类型；csv;xlsx |
| `version` | varchar(12) | 文件版本;20230213 |
| `serial_no` | int | 序列号;用于标记当前是第几个文件 |
| `status` | char(3) | 状态;I,W,CE,CS,UE,,US |
| `start_time` | timestamp | 开始时间;捞取数据的开始时间-包含 |
| `end_time` | timestamp | 结束时间;捞取数据的结束时间-不包含 |
| `total_count` | int | 回盘记录总数 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`task_id`
- `idx_create_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
