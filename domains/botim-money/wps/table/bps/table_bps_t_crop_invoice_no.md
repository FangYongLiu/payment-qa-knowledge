---
id: tbl_bps_t_crop_invoice_no
object_type: Table
name: corporate invoice no (t_crop_invoice_no)
aliases: [t_crop_invoice_no, bps.t_crop_invoice_no]
domain: wps
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: bps schema DDL
tags: [wps, bps]
sensitivity: normal
related_services: []
---

# corporate invoice no (t_crop_invoice_no)

## 用途
物理表 `bps.t_crop_invoice_no`,主键 `id`。corporate invoice no。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | ulid |
| `invoice_no` | varchar(32) | invoice no |
| `suffix` | int(5) | suffix |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
