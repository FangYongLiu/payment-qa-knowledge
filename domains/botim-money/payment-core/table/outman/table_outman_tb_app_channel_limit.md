---
id: tbl_outman_tb_app_channel_limit
object_type: Table
name: 渠道限制表 (tb_app_channel_limit)
aliases: [tb_app_channel_limit, outman.tb_app_channel_limit]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: outman schema DDL
tags: [payment-core, outman]
sensitivity: normal
related_services: []
---

# 渠道限制表 (tb_app_channel_limit)

## 用途
物理表 `outman.tb_app_channel_limit`,主键 `LIMIT_ID`。渠道限制表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `LIMIT_ID` | bigint(32) | 渠道限制编号 |
| `APP_ID` | bigint(32) | 应用编号 |
| `CHANNEL_TYPE` | varchar(32) | channel_id |
| `LIMIT` | varchar(256) | 渠道限额,使用json数据结构存储 |
| `MEMO` | varchar(256) | memo · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`LIMIT_ID`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
