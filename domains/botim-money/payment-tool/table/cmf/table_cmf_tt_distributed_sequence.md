---
id: tbl_cmf_tt_distributed_sequence
object_type: Table
name: tt_distributed_sequence (tt_distributed_sequence)
aliases: [tt_distributed_sequence, cmf.tt_distributed_sequence]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cmf schema DDL
tags: [payment-tool, cmf]
sensitivity: normal
related_services: []
---

# tt_distributed_sequence (tt_distributed_sequence)

## 用途
物理表 `cmf.tt_distributed_sequence`,主键 `SEQ_TICKET`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `SEQ_TICKET` | varchar(64) | 标识,一般用表名+记录ID表示 |
| `SEQ_NAME` | varchar(64) | 序列名称 · 可空 |
| `SEQ_VAL` | decimal(20) | 序列计数 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 · 可空 |

## 主键 / 索引
- 主键:`SEQ_TICKET`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
