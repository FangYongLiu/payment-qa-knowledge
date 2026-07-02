---
id: tbl_eminstalment_t_bill
object_type: Table
name: 帐单表 (t_bill)
aliases: [t_bill, eminstalment.t_bill]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: eminstalment schema DDL
tags: [lending, eminstalment]
sensitivity: normal
related_services: []
---

# 帐单表 (t_bill)

## 用途
物理表 `eminstalment.t_bill`,主键 `id`。帐单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `status` | int | 状态: 0：待生效，1： 待还款 2  结清 ,-1:取消（未付首付前订单取消） |
| `period_num` | int | 第几期 |
| `due_time` | timestamp | 到期还款日期 · 可空 |
| `finish_repay_time` | timestamp | 完结日期 · 可空 |
| `user_id` | varchar(32) | 用户ID |
| `principal` | decimal(15, 2) | 应还本金 |
| `instalment_fee` | decimal(15, 2) | 应还利息 |
| `currency` | char(3) | 货币 |
| `instalment_order_no` | varchar(64) | 分期支付订单号，对应t_instalment_order表的order_no |
| `create_time` | timestamp | 创建日期 |
| `update_time` | timestamp | 修改日期 |
| `start_accrue_fee_time` | timestamp | 开始收intalment_fee的时间,取值上一期bill的due_time，第一期取bill创建时间，含义是过了这个时间值在还款是要收instalment_fee的 |
| `type` | smallint(4) | 待补 |

## 主键 / 索引
- 主键:`id`
- `idx_order_no`:instalment_order_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
