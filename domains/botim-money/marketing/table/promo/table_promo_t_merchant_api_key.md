---
id: tbl_promo_t_merchant_api_key
object_type: Table
name: The API Key for the app of a merchant (t_merchant_api_key)
aliases: [t_merchant_api_key, promo.t_merchant_api_key]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: promo schema DDL
tags: [marketing, promo]
sensitivity: normal
related_services: []
---

# The API Key for the app of a merchant (t_merchant_api_key)

## 用途
物理表 `promo.t_merchant_api_key`,主键 `id`。The API Key for the app of a merchant。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | 待补 |
| `merchant_id` | varchar(32) | 待补 |
| `api_key` | varchar(64) | 待补 |
| `api_secret` | varchar(256) | 待补 |
| `level` | varchar(20) | API Key Level: Root, Merchant, Service |
| `status` | varchar(10) | the merchant found status: Active, Inactive |
| `view_times` | int | the api_secret only viewed if the view_times = 0 |
| `create_at` | timestamp | 待补 |
| `update_at` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
