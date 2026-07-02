---
id: tbl_cmf_tm_sys_configuration
object_type: Table
name: 系统配置 (tm_sys_configuration)
aliases: [tm_sys_configuration, cmf.tm_sys_configuration]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cmf schema DDL
tags: [payment-tool, cmf]
sensitivity: normal
related_services: []
---

# 系统配置 (tm_sys_configuration)

## 用途
物理表 `cmf.tm_sys_configuration`,主键 `ATTR_NAME`。系统配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ATTR_NAME` | varchar(32) | 配置项Key |
| `ATTR_VALUE` | varchar(512) | 取值 · 可空 |
| `MEMO` | varchar(128) | 说明 · 可空 |
| `GMT_CREATED` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后一次更新时间 |

## 主键 / 索引
- 主键:`ATTR_NAME`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
