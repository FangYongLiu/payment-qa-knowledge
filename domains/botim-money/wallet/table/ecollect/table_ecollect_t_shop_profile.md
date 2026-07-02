---
id: tbl_ecollect_t_shop_profile
object_type: Table
name: Shop brand profile (t_shop_profile)
aliases: [t_shop_profile, ecollect.t_shop_profile]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ecollect schema DDL
tags: [wallet, ecollect]
sensitivity: normal
related_services: []
---

# Shop brand profile (t_shop_profile)

## 用途
物理表 `ecollect.t_shop_profile`,主键 `shop_id`。Shop brand profile。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `shop_id` | bigint(21) | Shop ID |
| `home_template` | varchar(20) | Shop Home template |
| `avatar` | varchar(255) | Shop avatar · 可空 |
| `shop_name` | varchar(64) | Shop name |
| `description` | varchar(500) | Shop description · 可空 |
| `category` | varchar(32) | Shop category · 可空 |
| `create_by` | varchar(8) | Creator Botim UID |
| `create_time` | timestamp | Create time |
| `update_by` | varchar(8) | Updater Botim UID · 可空 |
| `update_time` | timestamp | Update time · 可空 |

## 主键 / 索引
- 主键:`shop_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
