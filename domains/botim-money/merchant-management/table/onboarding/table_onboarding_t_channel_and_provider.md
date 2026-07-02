---
id: tbl_onboarding_t_channel_and_provider
object_type: Table
name: payChannel and fundprovider relation (t_channel_and_provider)
aliases: [t_channel_and_provider, onboarding.t_channel_and_provider]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: onboarding schema DDL
tags: [merchant-management, onboarding]
sensitivity: normal
related_services: []
---

# payChannel and fundprovider relation (t_channel_and_provider)

## 用途
物理表 `onboarding.t_channel_and_provider`,主键 `id`。payChannel and fundprovider relation。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `fund_provider_code` | varchar(50) | id |
| `pay_channel` | varchar(50) | payChannel |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
