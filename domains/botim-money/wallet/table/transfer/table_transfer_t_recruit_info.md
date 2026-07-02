---
id: tbl_transfer_t_recruit_info
object_type: Table
name: 待招领 (t_recruit_info)
aliases: [t_recruit_info, transfer.t_recruit_info]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: transfer schema DDL
tags: [wallet, transfer]
sensitivity: normal
related_services: []
---

# 待招领 (t_recruit_info)

## 用途
物理表 `transfer.t_recruit_info`,主键 `id`。待招领。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `payment_no` | bigint(18) | 凭证号 |
| `identity_type` | varchar(20) | 标示类型(MOBILE/UID) · 可空 |
| `identity` | varchar(32) | 标示 |
| `partner_id` | varchar(32) | 商户号 · 可空 |
| `member_id` | varchar(30) | 会员ID · 可空 |
| `notify_partner_id` | varchar(32) | 默认通知平台 · 可空 |
| `nickname` | varchar(32) | 主题 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_identity_payment_no`:identity, payment_no
- `idx_recruit_payment_no`:payment_no

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
