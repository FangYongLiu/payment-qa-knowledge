---
id: tbl_promo_t_merchant_service
object_type: Table
name: Applications for Business Merchant (t_merchant_service)
aliases: [t_merchant_service, promo.t_merchant_service]
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

# Applications for Business Merchant (t_merchant_service)

## 用途
物理表 `promo.t_merchant_service`,主键 `id`。Applications for Business Merchant。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | 待补 |
| `merchant_id` | varchar(32) | the merchant id who owns the app |
| `service_code` | varchar(30) | MQ event service code |
| `service_name` | varchar(50) | the application name |
| `service_description` | varchar(300) | 待补 |
| `status` | varchar(10) | the app status: Active, Inactive |
| `create_at` | timestamp | 待补 |
| `update_at` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `u_merchant_app_name`:merchant_id, service_name (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
