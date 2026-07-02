---
id: tbl_custom_t_route_config
object_type: Table
name: t_route_config (t_route_config)
aliases: [t_route_config, custom.t_route_config]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: custom schema DDL
tags: [activation, custom]
sensitivity: normal
related_services: []
---

# t_route_config (t_route_config)

## 用途
物理表 `custom.t_route_config`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `custom_page` | varchar(16) | 定制页面 · 可空 |
| `merchant_group_id` | bigint(18) | 商户组id · 可空 |
| `pay_scene` | varchar(32) | 支付场景 · 可空 |
| `biz_product_code` | varchar(16) | 业务产品码 · 可空 |
| `platform` | varchar(32) | 入口类型 · 可空 |
| `route_condition` | varchar(150) | 路由条件 · 可空 |
| `topic_id` | bigint(18) | 方案id |
| `create_time` | timestamp | 创建时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
