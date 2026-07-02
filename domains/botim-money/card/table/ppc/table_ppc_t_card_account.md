---
id: tbl_ppc_t_card_account
object_type: Table
name: Card Account (t_card_account)
aliases: [t_card_account, ppc.t_card_account]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppc schema DDL
tags: [card, ppc]
sensitivity: normal
related_services: []
---

# Card Account (t_card_account)

## 用途
物理表 `ppc.t_card_account`,主键 `account_id`。Card Account。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `account_id` | bigint | Account ID: 8-digit date plus 9-digit serial number |
| `virtual_card_id` | bigint | Virtual Card ID |
| `currency_code` | char(3) | Currency Code |
| `account_status` | char(2) | Account Status: AW=Adding YSE wallet, AA=Adding member account, S=Success |
| `account_no` | varchar(32) | Account Number · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`account_id`
- `uk_virtual_card_id_currency`:virtual_card_id, currency_code (UNIQUE)
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
