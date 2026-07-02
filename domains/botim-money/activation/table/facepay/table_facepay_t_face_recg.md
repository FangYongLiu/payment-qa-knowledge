---
id: tbl_facepay_t_face_recg
object_type: Table
name: 特殊数据表 (t_face_recg)
aliases: [t_face_recg, facepay.t_face_recg]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: facepay schema DDL
tags: [activation, facepay]
sensitivity: normal
related_services: []
---

# 特殊数据表 (t_face_recg)

## 用途
物理表 `facepay.t_face_recg`,主键 `id`。特殊数据表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 |
| `authorisation_id` | bigint(18) | 支付授权表Id |
| `feature_data` | mediumtext | 授权类型 |
| `feature_type` | varchar(32) | 授权类型 |
| `feature_version` | varchar(32) | 授权类型 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `gmt_created` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
