---
id: tbl_collection_t_col_collection_ext
object_type: Table
name: 分案扩展信息表 记录分案时部分快照信息 (t_col_collection_ext)
aliases: [t_col_collection_ext, collection.t_col_collection_ext]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 分案扩展信息表 记录分案时部分快照信息 (t_col_collection_ext)

## 用途
物理表 `collection.t_col_collection_ext`,主键 `id`。分案扩展信息表 记录分案时部分快照信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(10) | 主健 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `bill_no` | varchar(64) | 账单号 |
| `collection_uid` | varchar(64) | 对应的分案uid |
| `total_will_repay_capital` | decimal(19, 2) | 总计应还本金 以放款方orderNo角度计算 · 可空 |
| `total_will_repay_fee` | decimal(19, 2) | 总计应还手续费 以放款方orderNo角度计算 · 可空 |
| `total_will_repay_penalty` | decimal(19, 2) | 总计应还罚息 以放款方orderNo角度计算 · 可空 |
| `total_already_repay_capital` | decimal(19, 2) | 总计已还本金 以放款方orderNo角度计算 · 可空 |
| `total_already_repay_fee` | decimal(19, 2) | 总计已还手续费 以放款方orderNo角度计算 · 可空 |
| `total_already_repay_penalty` | decimal(19, 2) | 总计已还利息 以放款方orderNo角度计算 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_bill_no`:bill_no
- `idx_collection_uid`:collection_uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
