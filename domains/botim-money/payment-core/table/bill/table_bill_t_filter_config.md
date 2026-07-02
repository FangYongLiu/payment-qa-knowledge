---
id: tbl_bill_t_filter_config
object_type: Table
name: filter_config (t_filter_config)
aliases: [t_filter_config, bill.t_filter_config]
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

# filter_config (t_filter_config)

## 用途
物理表 `bill.t_filter_config`,主键 `filter_config_id`。filter_config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `filter_config_id` | int | Data filter id · 可空 |
| `filter_code` | varchar(32) | Filter Code |
| `data_filter` | varchar(2048) | Data filter |
| `biz_product_code_list` | varchar(2048) | Biz Product Code List · 可空 |
| `enable_flag` | char | Enable flag: Y=Yes，N=No |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`filter_config_id`
- `uk_filter_code`:filter_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
