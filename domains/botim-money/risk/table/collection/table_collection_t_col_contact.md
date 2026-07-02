---
id: tbl_collection_t_col_contact
object_type: Table
name: 借款人通讯录 (t_col_contact)
aliases: [t_col_contact, collection.t_col_contact]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 借款人通讯录 (t_col_contact)

## 用途
物理表 `collection.t_col_contact`,主键 `id`。借款人通讯录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主健 · 可空 |
| `create_by` | varchar(255) | 创建者 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `update_by` | varchar(100) | 更新人员 · 可空 |
| `member_id` | varchar(64) | id |
| `name` | varchar(64) | 联系人姓名 · 可空 |
| `type` | tinyint(5) | 1本人 2紧急联系人 3uae联系人 4非uae联系人 |
| `is_new` | tinyint(5) | 是否最新 · 可空 |
| `product` | tinyint(5) | 产品类型 · 可空 |
| `sort` | int(5) | 排序1最前展示 |
| `phone` | varchar(50) | 完整电话 · 可空 |
| `simple_phone` | varchar(50) | 电话 · 可空 |
| `prefix` | varchar(50) | 电话区号 · 可空 |
| `relative` | varchar(50) | 关系 · 可空 |
| `invalid` | tinyint | 0无效 1有效 |

## 主键 / 索引
- 主键:`id`
- `idx_member_id`:member_id
- `idx_phone`:phone

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
