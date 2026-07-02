---
id: tbl_router_t_channel
object_type: Table
name: 渠道表 (t_channel)
aliases: [t_channel, router.t_channel]
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

# 渠道表 (t_channel)

## 用途
物理表 `router.t_channel`,主键 `channel_code`。渠道表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `channel_code` | varchar(32) | 渠道编号 |
| `channel_name` | varchar(32) | 渠道名称 · 可空 |
| `biz_type` | varchar(1) | 业务类型 · 可空 |
| `pay_mode` | varchar(16) | 支付方式 · 可空 |
| `channel_type` | varchar(10) | 渠道类型 · 可空 |
| `inst_code` | varchar(16) | 渠道所属机构 · 可空 |
| `status` | char | 状态 · 可空 |
| `memo` | varchar(32) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `fund_provider_code` | varchar(12) | fund_provider_code · 可空 |
| `register_rule` | varchar(32) | if not empty,the transaction needs to check whether the reporting is completed according to the rules · 可空 |

## 主键 / 索引
- 主键:`channel_code`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
