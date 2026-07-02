---
id: tbl_bill_t_bill_detail_url_config
object_type: Table
name: bill_detail_url_config (t_bill_detail_url_config)
aliases: [t_bill_detail_url_config, bill.t_bill_detail_url_config]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: bill schema DDL
tags: [payment-core, bill]
sensitivity: normal
related_services: []
---

# bill_detail_url_config (t_bill_detail_url_config)

## 用途
物理表 `bill.t_bill_detail_url_config`,主键 `config_id`。bill_detail_url_config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `config_id` | int | ID · 可空 |
| `partner_id` | varchar(32) | partner id |
| `biz_product_code` | varchar(32) | business product code |
| `payment_type` | varchar(32) | payment type |
| `client_id` | varchar(32) | client id |
| `match_expression` | varchar(255) | match expression: true,false · 可空 |
| `url_expression` | varchar(255) | Url expression |
| `enable_flag` | char | Enable flag: Y=Yes，N=No |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`config_id`
- `uk_partner_code_payment_client_match`:partner_id, biz_product_code, payment_type, client_id, match_expression (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
