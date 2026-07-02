---
id: tbl_visii_t_vam_extra
object_type: Table
name: Vam Extra (t_vam_extra)
aliases: [t_vam_extra, visii.t_vam_extra]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: visii schema DDL
tags: [deposit-vam, visii]
sensitivity: normal
related_services: []
---

# Vam Extra (t_vam_extra)

## 用途
物理表 `visii.t_vam_extra`,主键 `extra_id`。Vam Extra。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `extra_id` | bigint(19) | extra id |
| `reference_id` | bigint(19) | reference id |
| `type` | char | type,  |
| `fragment` | int | fragment 1- |
| `data` | varchar(512) | data |
| `gmt_create` | timestamp(3) | create time |

## 主键 / 索引
- 主键:`extra_id`
- `uk_refid_type_fragment`:reference_id, type, fragment (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
