---
id: tbl_remittance_t_channel_sftp_config
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
- t_channel_sftp_config
subdomain: remittance
module: null
sensitivity: normal
name: 渠道SFTP配置(t_channel_sftp_config)
aliases:
- t_channel_sftp_config
related_services:
- svc_remittance
related_scenarios: []
---
# 渠道SFTP配置(t_channel_sftp_config)

## 用途
渠道SFTP配置。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | ID |
| `channel_code` | varchar(7) | NOT NULL | 渠道CODE |
| `biz_type` | varchar(12) | NOT NULL | 业务类型 |
| `sftp_url` | varchar(32) |  | sftp路径 |
| `port` | int(8) |  | 端口 |
| `username` | varchar(64) |  | 用户名 |
| `password` | varchar(64) |  | 密码 |
| `file_dir` | varchar(100) |  | 文件目录;捞取数据的开始时间-包含 |
| `file_name_rule` | varchar(100) |  | 文件名称规则;捞取数据的结束时间-不包含 |
| `file_encoding` | varchar(16) |  | 文件编码 |
| `status` | char(3) |  | 状态;I,W,CE,CS,UE,,US |
| `operator` | varchar(32) |  | 造作者 |
| `remark` | varchar(255) |  | 备注 |
| `private_key_ticket` | varchar(1024) |  | 密钥ues标志 |
| `private_key_pass_ticket` | varchar(1024) |  | 密钥密码ues标志 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
