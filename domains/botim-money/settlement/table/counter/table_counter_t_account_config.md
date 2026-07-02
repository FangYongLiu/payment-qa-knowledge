---
id: tbl_counter_t_account_config
object_type: Table
name: 账号配置表 (t_account_config)
aliases: [t_account_config, counter.t_account_config]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: counter schema DDL
tags: [settlement, counter]
sensitivity: normal
related_services: []
---

# 账号配置表 (t_account_config)

## 用途
物理表 `counter.t_account_config`,主键 `account_id`。账号配置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `account_id` | bigint(17) | 账号id · 可空 |
| `account_name` | varchar(32) | 账户名称 |
| `account_no` | varchar(32) | 账户编号 |
| `bank_code` | varchar(16) | 银行编码 |
| `bank_name` | varchar(32) | 银行名称 |
| `alias` | varchar(32) | 别名 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`account_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
