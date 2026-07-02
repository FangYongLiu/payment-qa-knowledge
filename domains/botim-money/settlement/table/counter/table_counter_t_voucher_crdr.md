---
id: tbl_counter_t_voucher_crdr
object_type: Table
name: 凭证借贷方 (t_voucher_crdr)
aliases: [t_voucher_crdr, counter.t_voucher_crdr]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: counter schema DDL
tags: [settlement, counter]
sensitivity: normal
related_services: []
---

# 凭证借贷方 (t_voucher_crdr)

## 用途
物理表 `counter.t_voucher_crdr`,主键 `crdr_id`。凭证借贷方。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `crdr_id` | bigint(17) | 借贷id · 可空 |
| `voucher_id` | bigint(17) | 凭证id |
| `direction` | varchar(16) | 方向：正向-positive、反向-negative |
| `member_id` | varchar(32) | 会员id |
| `account_no` | varchar(32) | 账户编号 |
| `fund_type` | varchar(5) | 借记资金属性：CA-贷方资金 DA-借方资金 BI-借贷均可 |

## 主键 / 索引
- 主键:`crdr_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
