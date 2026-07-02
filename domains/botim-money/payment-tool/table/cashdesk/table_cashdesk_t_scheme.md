---
id: tbl_cashdesk_t_scheme
object_type: Table
name: 方案 (t_scheme)
aliases: [t_scheme, cashdesk.t_scheme]
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

# 方案 (t_scheme)

## 用途
物理表 `cashdesk.t_scheme`,主键 `scheme_code`。方案。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `scheme_code` | bigint | 方案code |
| `scheme_name` | varchar(120) | 方案名称 |
| `scheme_desc` | varchar(150) | 方案描述 · 可空 |
| `platform_type` | varchar(20) | 支持平台 |
| `host_app` | varchar(32) | 载体code |
| `pay_scene` | varchar(100) | 支持场景 |
| `withhold_flag` | varchar(10) | 带扣标记 · 可空 |
| `memo` | varchar(128) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`scheme_code`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
