---
id: tbl_cctransfer_t_transfer_order_participant
object_type: Table
name: 转账参与者 (t_transfer_order_participant)
aliases: [t_transfer_order_participant, cctransfer.t_transfer_order_participant]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cctransfer schema DDL
tags: [crypto, cctransfer]
sensitivity: normal
related_services: []
---

# 转账参与者 (t_transfer_order_participant)

## 用途
物理表 `cctransfer.t_transfer_order_participant`,主键 `id`。转账参与者。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `member_id` | varchar(32) | 会员ID |
| `platform_id` | varchar(32) | status · 可空 |
| `alias_name` | varchar(128) | 别名 · 可空 |
| `role` | varchar(16) | 错误原因 |
| `transfer_order_id` | bigint | 转账订单号 |
| `mobile_no_ticket` | varchar(32) | 手机号ticket · 可空 |
| `nick_name` | varchar(256) | 昵称 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_top_mt`:member_id, transfer_order_id (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
