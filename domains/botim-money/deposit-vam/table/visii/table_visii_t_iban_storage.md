---
id: tbl_visii_t_iban_storage
object_type: Table
name: unique iban (t_iban_storage)
aliases: [t_iban_storage, visii.t_iban_storage]
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

# unique iban (t_iban_storage)

## 用途
物理表 `visii.t_iban_storage`,主键 `storage_id`。unique iban。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `storage_id` | bigint | Iban Storage Id · 可空 |
| `request_no` | varchar(32) | Request no |
| `bank_code` | varchar(5) | Bank Code,PAYBY,ZAND · 可空 |
| `iban_type` | char | Iban Type · 可空 |
| `iban` | varchar(32) | iban · 可空 |
| `status` | char | status,F-ForAllocate，L-Lock，I-Invalid，A-Allocated |
| `memo` | varchar(64) | Memo · 可空 |
| `extension` | varchar(64) | Extension · 可空 |
| `gmt_create` | timestamp(3) | Create Time |
| `gmt_modified` | timestamp(3) | Modify Time · 可空 |

## 主键 / 索引
- 主键:`storage_id`
- `idx_iban_request_batch_no`:request_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
