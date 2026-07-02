---
id: tbl_pcbs_t_daily_file
object_type: Table
name: Daily File (t_daily_file)
aliases: [t_daily_file, pcbs.t_daily_file]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pcbs schema DDL
tags: [settlement, pcbs]
sensitivity: normal
related_services: []
---

# Daily File (t_daily_file)

## 用途
物理表 `pcbs.t_daily_file`,主键 `file_id`。Daily File。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `file_id` | bigint | File ID |
| `partner_id` | varchar(20) | Partner ID |
| `file_code` | varchar(10) | File Code: CDB=Customer Daily Balance, DP=Daily Profit |
| `file_date` | varchar(8) | File Date: YYYYMMDD |
| `file_status` | varchar(2) | File Status: I=Init, US=Upload Success, PF=Process Fail, S=Process Success |
| `sftp_file_path` | varchar(200) | SFTP File Path |
| `ufs_file_path` | varchar(200) | UFS File Path · 可空 |
| `error_message` | varchar(100) | Error Message · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`file_id`
- `uk_date_partner_filecode`:file_date, partner_id, file_code (UNIQUE)
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
