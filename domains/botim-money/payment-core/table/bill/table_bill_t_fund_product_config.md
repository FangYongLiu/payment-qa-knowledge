---
id: tbl_bill_t_fund_product_config
object_type: Table
name: t_fund_product_config (t_fund_product_config)
aliases: [t_fund_product_config, bill.t_fund_product_config]
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

# t_fund_product_config (t_fund_product_config)

## 用途
物理表 `bill.t_fund_product_config`,主键 `product_config_id`。t_fund_product_config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `product_config_id` | int | Config id · 可空 |
| `biz_product_code` | varchar(32) | Biz Product Code |
| `clearing_code` | varchar(32) | Clearing Code |
| `direction` | varchar(32) | Direction: positive,negative |
| `fund_memo` | varchar(32) | Fund memo |
| `description` | varchar(512) | Description |
| `enable_flag` | char | Enable flag: Y=Yes，N=No |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(100) | Fund Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`product_config_id`
- `uk_product_clearing_direction_fundmemo`:biz_product_code, clearing_code, direction, fund_memo (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
