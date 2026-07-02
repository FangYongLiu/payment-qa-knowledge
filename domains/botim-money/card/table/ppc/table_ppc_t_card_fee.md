---
id: tbl_ppc_t_card_fee
object_type: Table
name: Card Fee (t_card_fee)
aliases: [t_card_fee, ppc.t_card_fee]
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

# Card Fee (t_card_fee)

## 用途
物理表 `ppc.t_card_fee`,主键 `fee_request_no`。Card Fee。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `fee_request_no` | bigint | Fee Request No: Trade Request No, 凭证号 |
| `virtual_card_id` | bigint | Virtual Card ID: Virtual Card ID |
| `member_id` | varchar(20) | Member ID |
| `fee_type` | varchar(8) | Fee Type: APC=Apply Physical Card, CC=Close Card |
| `fee_amount` | decimal(19, 4) | Fee Amount |
| `currency` | char(3) | Fee Currency |
| `status` | varchar(10) | Card Fee Status: W=Waiting, S=Succeed, C=Close, RF=Refunding, RD=Refunded |
| `relate_id` | bigint | Relate ID · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp(3) | Create time |
| `update_time` | timestamp(3) | Update time |
| `refund_request_no` | bigint | Refund Request No · 可空 |
| `paid_time` | timestamp(3) | Paid Time · 可空 |

## 主键 / 索引
- 主键:`fee_request_no`
- `idx_paid_time`:paid_time
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
