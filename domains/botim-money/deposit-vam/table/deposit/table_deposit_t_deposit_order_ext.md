---
id: tbl_deposit_t_deposit_order_ext
object_type: Table
name: 充值交易订单扩展表 (t_deposit_order_ext)
aliases: [t_deposit_order_ext, deposit.t_deposit_order_ext]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: deposit schema DDL
tags: [deposit-vam, deposit]
sensitivity: normal
related_services: []
---

# 充值交易订单扩展表 (t_deposit_order_ext)

## 用途
物理表 `deposit.t_deposit_order_ext`,主键 `TRADE_VOUCHER_NO`。充值交易订单扩展表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `TRADE_VOUCHER_NO` | varchar(32) | 交易凭证号，主键，统一凭证 |
| `client_id` | varchar(32) | 调用方标识 · 可空 |
| `fee_bearer` | varchar(32) | Fee Bearer · 可空 |
| `bearer_account_type` | varchar(16) | Fee Bearer Account Type · 可空 |
| `bearer_account_no` | varchar(32) | Fee Bearer Account No · 可空 |

## 主键 / 索引
- 主键:`TRADE_VOUCHER_NO`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
