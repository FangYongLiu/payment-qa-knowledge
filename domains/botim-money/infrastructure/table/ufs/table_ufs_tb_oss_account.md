---
id: tbl_ufs_tb_oss_account
object_type: Table
name: 账户表 (tb_oss_account)
aliases: [tb_oss_account, ufs.tb_oss_account]
domain: infrastructure
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ufs schema DDL
tags: [infrastructure, ufs]
sensitivity: normal
related_services: []
---

# 账户表 (tb_oss_account)

## 用途
物理表 `ufs.tb_oss_account`,主键 `account_id`。账户表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `account_id` | int | 账户id · 可空 |
| `oss_type` | varchar(32) | aliyun-阿里云，huaweicloud-华为云 · 可空 |
| `account_no` | varchar(32) | 账户号 · 可空 |
| `accesskey_id` | varchar(32) | 访问key的id · 可空 |
| `accesskey_secret` | varchar(32) | 访问key的secret · 可空 |
| `bucket_alias` | varchar(100) | bucket别名 · 可空 |
| `bucket` | varchar(128) | oss的命名空间名 · 可空 |
| `url` | varchar(128) | 访问地址 · 可空 |
| `status` | char | 账户状态 N-正常D-删除 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `bucket_access` | varchar(32) | 待补 |
| `internal_url` | varchar(128) | 内网访问地址 · 可空 |

## 主键 / 索引
- 主键:`account_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
