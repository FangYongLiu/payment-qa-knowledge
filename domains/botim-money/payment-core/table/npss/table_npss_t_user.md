---
id: tbl_npss_t_user
object_type: Table
name: 用户eid唯一索引 (t_user)
aliases: [t_user, npss.t_user]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: npss schema DDL
tags: [payment-core, npss]
sensitivity: normal
related_services: []
---

# 用户eid唯一索引 (t_user)

## 用途
物理表 `npss.t_user`,主键 `member_id`。用户eid唯一索引。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `member_id` | varchar(20) | 用户id |
| `name` | varchar(64) | 用户名 |
| `mobile_no` | varchar(20) | 手机号 · 可空 |
| `eid` | varchar(20) | eid · 可空 |
| `birth_date` | date | 出生日期 |
| `birth_city` | varchar(20) | 出生城市 |
| `birth_country` | char(2) | 出生国家 |
| `status` | char | 状态 |
| `memo` | varchar(64) | 备注 · 可空 |
| `extension` | varchar(512) | user extension · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`member_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
