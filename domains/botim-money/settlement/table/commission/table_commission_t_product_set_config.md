---
id: tbl_commission_t_product_set_config
object_type: Table
name: Product Set Config (t_product_set_config)
aliases: [t_product_set_config, commission.t_product_set_config]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: commission schema DDL
tags: [settlement, commission]
sensitivity: normal
related_services: []
---

# Product Set Config (t_product_set_config)

## 用途
物理表 `commission.t_product_set_config`,主键 `config_id`。Product Set Config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `config_id` | bigint | Config id · 可空 |
| `product_set_code` | varchar(10) | Product set code: ACQ=Acquire |
| `biz_product_codes` | varchar(100) | Biz product codes |
| `name` | varchar(50) | Name |
| `enable_flag` | char | Enable flag: Y=Yes，N=No |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`config_id`
- `uk_product_set_code`:product_set_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
