---
id: tbl_escrow_t_report_upload_method
object_type: Table
name: 报备上传方法 (t_report_upload_method)
aliases: [t_report_upload_method, escrow.t_report_upload_method]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: escrow schema DDL
tags: [deposit-vam, escrow]
sensitivity: normal
related_services: []
---

# 报备上传方法 (t_report_upload_method)

## 用途
物理表 `escrow.t_report_upload_method`,主键 `id`。报备上传方法。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(19) | id |
| `bank_code` | varchar(8) | 银行编号 · 可空 |
| `upload_type` | varchar(4) | 上报类型，E-email；S-sftp；A-api接口 |
| `account_info` | varchar(2048) | 账户信息 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modify` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
