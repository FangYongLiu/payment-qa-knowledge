---
id: tbl_npss_t_reconciliation_flow
object_type: Table
name: inst_order_no channel_code direction唯一索引 (t_reconciliation_flow)
aliases: [t_reconciliation_flow, npss.t_reconciliation_flow]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: npss schema DDL
tags: [payment-core, npss]
sensitivity: normal
related_services: []
---

# inst_order_no channel_code direction唯一索引 (t_reconciliation_flow)

## 用途
物理表 `npss.t_reconciliation_flow`,主键 `flow_id`。inst_order_no channel_code direction唯一索引。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `flow_id` | bigint(18) | 流水id |
| `inst_order_no` | varchar(64) | Inst Order No, eg.P2P0003P423000000006873 · 可空 |
| `channel_code` | varchar(10) | 渠道编号 |
| `amount` | decimal(19, 4) | 金额 |
| `currency` | char(3) | 币种 · 可空 |
| `status` | char | 状态,I-初始,S-发送成功,R-重试 |
| `direction` | char | 方向,I-入款,O-出款，B-退款 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`flow_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
