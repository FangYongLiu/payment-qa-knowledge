---
id: tbl_ppc_t_statement_apply
object_type: Table
name: Statement Apply (t_statement_apply)
aliases: [t_statement_apply, ppc.t_statement_apply]
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

# Statement Apply (t_statement_apply)

## 用途
物理表 `ppc.t_statement_apply`,主键 `apply_no`。Statement Apply。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `apply_no` | bigint | Apply Order No |
| `member_id` | varchar(20) | Member ID |
| `from_date` | date | From Date |
| `to_date` | date | To Date |
| `receive_email` | varchar(200) | Receive Email |
| `status` | char(2) | Status: W=Waiting, GF=Generate File, C=Closed, S=Success |
| `fee_amount` | decimal(19, 4) | Fee Amount |
| `currency` | char(3) | Currency |
| `virtual_card_id` | bigint | Virtual Card ID · 可空 |
| `file_info` | varchar(512) | File Info: Statement file info object with JSON format · 可空 |
| `delivery_detail` | varchar(32) | Delivery Detail: Delivery with Hard Copy · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`apply_no`
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
