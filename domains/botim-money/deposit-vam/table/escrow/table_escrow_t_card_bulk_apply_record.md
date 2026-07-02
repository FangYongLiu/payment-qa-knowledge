---
id: tbl_escrow_t_card_bulk_apply_record
object_type: Table
name: apply_reference 唯一索引 (t_card_bulk_apply_record)
aliases: [t_card_bulk_apply_record, escrow.t_card_bulk_apply_record]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: escrow schema DDL
tags: [deposit-vam, escrow]
sensitivity: normal
related_services: []
---

# apply_reference 唯一索引 (t_card_bulk_apply_record)

## 用途
物理表 `escrow.t_card_bulk_apply_record`,主键 `id`。apply_reference 唯一索引。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(19) | id |
| `apply_reference` | varchar(32) | 申请ID |
| `bank_code` | varchar(8) | 银行编号 |
| `apply_num` | int(8) | 申请数量 |
| `response_num` | int(8) | 响应数量 · 可空 |
| `response_code` | varchar(16) | 响应状态 · 可空 |
| `response_msg` | varchar(256) | 响应编码 · 可空 |
| `status` | varchar(4) | 申请状态，S-Success申请成功，F-Fail申请失败，P-Processing处理中，A-AWAIT待处理 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modify` | timestamp | 更新时间 · 可空 |
| `memo` | varchar(512) | memo · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
