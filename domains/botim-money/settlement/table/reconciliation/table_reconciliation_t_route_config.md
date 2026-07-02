---
id: tbl_reconciliation_t_route_config
object_type: Table
name: 渠道对账单下载方式路由 (t_route_config)
aliases: [t_route_config, reconciliation.t_route_config]
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

# 渠道对账单下载方式路由 (t_route_config)

## 用途
物理表 `reconciliation.t_route_config`,主键 `route_id`。渠道对账单下载方式路由。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `route_id` | int | 路由ID · 可空 |
| `route_name` | varchar(64) | 路由名称 · 可空 |
| `fund_channel_code` | varchar(32) | 渠道编号 · 可空 |
| `biz_type` | varchar(4) | 业务类型 · 可空 |
| `route_type` | varchar(8) | 类型 目前提供sftp、http方式 · 可空 |
| `status` | varchar(4) | 路由状态 · 可空 |
| `operator` | varchar(32) | 创建者 · 可空 |
| `weight` | int | 权重，同一渠道支持多个类型，权重优先 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`route_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
