---
id: tbl_rdgs_t_remittance_report_task
object_type: Table
name: t_remittance_report_task (t_remittance_report_task)
aliases: [t_remittance_report_task, rdgs.t_remittance_report_task]
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

# t_remittance_report_task (t_remittance_report_task)

## 用途
物理表 `rdgs.t_remittance_report_task`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键id |
| `channel_code` | varchar(20) | report channel code;MG |
| `report_category` | varchar(32) | 报表类别 |
| `upload_path` | varchar(255) | 上传/下载路径;上传/下载的文件路径 · 可空 |
| `file_name` | varchar(64) | 文件名称 · 可空 |
| `file_tag` | varchar(64) | 上传ufs的文件tag · 可空 |
| `file_suffix` | char(4) | 文件类型；csv;xlsx · 可空 |
| `version` | varchar(12) | 文件版本;202302130000 |
| `status` | char | 状态I，W，E，S |
| `start_time` | timestamp | 开始时间;捞取数据的开始时间-包含 |
| `end_time` | timestamp | 结束时间;捞取数据的结束时间-不包含 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `remaining_retry_times` | int | 剩余异常重试次数 · 可空 |
| `total_count` | int(12) | 总条数 · 可空 |
| `total_amount` | decimal(19, 4) | 汇款总金额 · 可空 |
| `extension` | varchar(255) | 扩展参数 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_create_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
