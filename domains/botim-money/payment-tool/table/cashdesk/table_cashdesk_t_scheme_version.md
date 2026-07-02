---
id: tbl_cashdesk_t_scheme_version
object_type: Table
name: 方案与版本 (t_scheme_version)
aliases: [t_scheme_version, cashdesk.t_scheme_version]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cashdesk schema DDL
tags: [payment-tool, cashdesk]
sensitivity: normal
related_services: []
---

# 方案与版本 (t_scheme_version)

## 用途
物理表 `cashdesk.t_scheme_version`,主键 `id`。方案与版本。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `scheme_code` | bigint | 方案code |
| `platform_type` | varchar(20) | 平台类型:IOS,ANDROID,WEB,H5 |
| `host_app` | varchar(20) | 宿主平台:payby,totok,bootim |
| `min_version` | int(10) | 最小版本:1 |
| `max_version` | int(10) | 最大版本:999999 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
