---
id: tbl_eminstalment_t_contact
object_type: Table
name: 联系人信息表 (t_contact)
aliases: [t_contact, eminstalment.t_contact]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: eminstalment schema DDL
tags: [lending, eminstalment]
sensitivity: normal
related_services: []
---

# 联系人信息表 (t_contact)

## 用途
物理表 `eminstalment.t_contact`,主键 `id`。联系人信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `user_id` | varchar(20) | 用户id |
| `contact_type` | smallint(4) | 1、第一紧急联系人 |
| `name` | varchar(200) | 联系人名称 |
| `mobile_prefix` | varchar(16) | 联系人电话国家码 |
| `phone` | varchar(16) | 联系人电话号码 |
| `relative` | varchar(32) | 联系人与申请人的关系 |
| `version` | int | 某用户、某contact_type 下维护的联系人的版本号，用于记录数据变动 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_v`:user_id, contact_type, version (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
