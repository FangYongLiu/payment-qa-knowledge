---
id: tbl_cashdesk_t_merchant_config
object_type: Table
name: 商户配置表 (t_merchant_config)
aliases: [t_merchant_config, cashdesk.t_merchant_config]
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

# 商户配置表 (t_merchant_config)

## 用途
物理表 `cashdesk.t_merchant_config`,主键 `id`。商户配置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 |
| `merchant_id` | varchar(18) | 商户id · 可空 |
| `channel_env` | char | 渠道环境（T:真实渠道  M：mock渠道） |
| `gmt_created` | timestamp | 创建时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
