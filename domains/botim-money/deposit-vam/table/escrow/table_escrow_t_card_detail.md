---
id: tbl_escrow_t_card_detail
object_type: Table
name: cardId唯一索引 (t_card_detail)
aliases: [t_card_detail, escrow.t_card_detail]
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

# cardId唯一索引 (t_card_detail)

## 用途
物理表 `escrow.t_card_detail`,主键 `id`。cardId唯一索引。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(19) | id · 可空 |
| `card_no` | varchar(32) | 卡号 |
| `bank_code` | varchar(32) | 银行编号， 区分银行的标识 |
| `card_type` | varchar(4) | 卡类型，C-Common普通卡, S-Special靓号卡. |
| `status` | varchar(4) | 卡状态，F-For allocate未分配;L-Lock锁定；I-Invalid失效；A-Allocated已分配 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modify` | timestamp | 修改时间 · 可空 |
| `embossed_english` | varchar(255) | 卡上的姓名 |
| `card_id` | varchar(128) | 卡号 · 可空 |
| `request_reference` | varchar(32) | 申请编号 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_card_type_status_gmtcreate`:card_type, status, gmt_create
- `idx_gmt_create`:gmt_create

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
