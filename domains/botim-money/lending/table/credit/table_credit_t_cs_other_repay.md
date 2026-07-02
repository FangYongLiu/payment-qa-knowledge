---
id: tbl_credit_t_cs_other_repay
object_type: Table
name: 其它还款类型记录 (t_cs_other_repay)
aliases: [t_cs_other_repay, credit.t_cs_other_repay]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# 其它还款类型记录 (t_cs_other_repay)

## 用途
物理表 `credit.t_cs_other_repay`,主键 `id`。其它还款类型记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `status` | int | 状态: 0 初始化 1  完结 |
| `repay_way` | smallint(5) | 还款方式 |
| `amount` | decimal(15, 2) | 金额 |
| `user_id` | varchar(32) | 用户ID |
| `request_no` | varchar(64) | 流水ID |
| `repay_no` | varchar(64) | 还款ID · 可空 |
| `gid` | bigint | 支付凭证号 · 可空 |
| `order_no` | varchar(64) | 订单ID |
| `created_time` | timestamp | 创建日期 · 可空 |
| `last_modified` | timestamp | 修改日期 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_order_no`:order_no
- `idx_request_no`:request_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
