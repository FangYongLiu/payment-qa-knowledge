---
id: tbl_router_t_channel_api_param
object_type: Table
name: 渠道接口参数表 (t_channel_api_param)
aliases: [t_channel_api_param, router.t_channel_api_param]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: router schema DDL
tags: [payment-tool, router]
sensitivity: normal
related_services: []
---

# 渠道接口参数表 (t_channel_api_param)

## 用途
物理表 `router.t_channel_api_param`,主键 `param_id`。渠道接口参数表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `param_id` | int(32) | 参数id · 可空 |
| `api_code` | varchar(32) | 接口编码 · 可空 |
| `param_name` | varchar(32) | 参数名称 · 可空 |
| `is_origin` | char | 是否原订单参数, Y-原订单，N-非原订单 · 可空 |
| `scene` | varchar(10) | 场景:request-请求，response-响应 · 可空 |
| `memo` | varchar(32) | 备注 · 可空 |
| `extension` | varchar(128) | 扩展 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`param_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
