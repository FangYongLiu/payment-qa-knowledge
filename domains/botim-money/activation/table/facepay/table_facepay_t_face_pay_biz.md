---
id: tbl_facepay_t_face_pay_biz
object_type: Table
name: 业务表 (t_face_pay_biz)
aliases: [t_face_pay_biz, facepay.t_face_pay_biz]
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

# 业务表 (t_face_pay_biz)

## 用途
物理表 `facepay.t_face_pay_biz`,主键 `id`。业务表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 |
| `biz_id` | varchar(64) | 业务id |
| `face_img_base64` | mediumtext | 面部图片ba64 |
| `biz_status` | varchar(25) | 业务状态：Authorized,AidedPromotion,UnAuthorized |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `gmt_created` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
