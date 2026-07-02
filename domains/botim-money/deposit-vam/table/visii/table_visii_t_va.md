---
id: tbl_visii_t_va
object_type: Table
name: Virtual Iban (t_va)
aliases: [t_va, visii.t_va]
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

# Virtual Iban (t_va)

## 用途
物理表 `visii.t_va`,主键 `va_id`。Virtual Iban。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `va_id` | bigint(19) | va id |
| `request_no` | varchar(64) | unique request no, idempotency key · 可空 |
| `member_id` | varchar(20) | member id |
| `bank_code` | varchar(5) | Bank Code |
| `va_type` | char(2) | va type, VA-virtual account |
| `name` | varchar(128) | name |
| `iban` | varchar(20) | iban · 可空 |
| `id_type` | varchar(3) | Id Type, eid/p/tl · 可空 |
| `id_no` | varchar(20) | Id No · 可空 |
| `account_type` | varchar(10) | acct type,Basic/WPS_SALARY |
| `account_seq` | int(10) | Account seq |
| `status` | char | I/P/V/D |
| `message` | varchar(128) | result · 可空 |
| `result_code` | varchar(32) | result · 可空 |
| `extension` | varchar(255) | extension · 可空 |
| `gmt_create` | timestamp(3) | create time |
| `gmt_modified` | timestamp(3) | modify time · 可空 |
| `gmt_finished` | timestamp(3) | finish time · 可空 |
| `next_notify_time` | timestamp(3) | next todo card notify time · 可空 |
| `notify_status` | char | N-NO_NEED, P-PENDING, S-NOTIFIED, R-REMOVED · 可空 |

## 主键 / 索引
- 主键:`va_id`
- `uk_iBanNo`:iban (UNIQUE)
- `uk_memberId_accountType_bk`:member_id, bank_code, account_seq (UNIQUE)
- `uk_va_request_no`:member_id, request_no (UNIQUE)
- `idx_va_create`:gmt_create
- `idx_va_next_notify`:next_notify_time

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
