---
id: tbl_reconciliation_t_channel_sftp_config
object_type: Table
name: 渠道sftp配置 (t_channel_sftp_config)
aliases: [t_channel_sftp_config, reconciliation.t_channel_sftp_config]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# 渠道sftp配置 (t_channel_sftp_config)

## 用途
物理表 `reconciliation.t_channel_sftp_config`,主键 `id`。渠道sftp配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `fund_channel_code` | varchar(32) | 渠道编号 · 可空 |
| `biz_type` | varchar(8) | 业务类型 · 可空 |
| `sftp_url` | varchar(128) | SFTP Url · 可空 |
| `port` | varchar(16) | 端口 · 可空 |
| `username` | varchar(64) | 用户名 · 可空 |
| `password` | varchar(64) | 密码 · 可空 |
| `file_dir` | varchar(128) | 文件目录 · 可空 |
| `file_name_rule` | varchar(128) | 文件名称规则 · 可空 |
| `file_encoding` | varchar(16) | 文件编码 · 可空 |
| `status` | varchar(4) | 状态 · 可空 |
| `operator` | varchar(32) | 操作者 · 可空 |
| `remark` | varchar(256) | 备注 · 可空 |
| `private_key_ticket` | varchar(1024) | 密钥ues标志 · 可空 |
| `private_key_pass_ticket` | varchar(1024) | 密钥密码ues标志 · 可空 |
| `encryption_file_type` | varchar(8) | Encryption File Type · 可空 |
| `decryption_info` | varchar(255) | Decryption Information · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
