---
id: tbl_visii_t_relate_vam_order
object_type: Table
name: Relate Vam Order (t_relate_vam_order)
aliases: [t_relate_vam_order, visii.t_relate_vam_order]
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

# Relate Vam Order (t_relate_vam_order)

## 用途
物理表 `visii.t_relate_vam_order`,主键 `order_id`。Relate Vam Order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `order_id` | bigint | order id |
| `order_type` | varchar(10) | Order Type: FO-Fundout |
| `order_voucher_no` | bigint | order voucher no |
| `on_account_voucher_no` | bigint | on account voucher no · 可空 |
| `order_status` | char | Order Status: P-Processing, F-Fail, S-Success |
| `extension` | varchar(255) | Extension · 可空 |
| `gmt_create` | timestamp | Create Time |
| `gmt_modified` | timestamp | Update Time |

## 主键 / 索引
- 主键:`order_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
