---
id: tbl_vis_t_iban_account
object_type: Table
name: iban唯一索引 (t_iban_account)
aliases: [t_iban_account, vis.t_iban_account]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: vis schema DDL
tags: [deposit-vam, vis]
sensitivity: normal
related_services: []
---

# iban唯一索引 (t_iban_account)

## 用途
物理表 `vis.t_iban_account`,主键 `account_id`。iban唯一索引。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `account_id` | int(16) | 库存id · 可空 |
| `request_batch_no` | varchar(32) | 请求号 |
| `bank_code` | varchar(5) | Bank Code,PAYBY,FAB · 可空 |
| `iban_no` | varchar(32) | iban · 可空 |
| `status` | char | F-未分配，L-锁定，I-失效，A-已分配 |
| `memo` | varchar(64) | 备注 · 可空 |
| `extension` | varchar(64) | 扩展 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`account_id`
- `idx_iban_request_batch_no`:request_batch_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
