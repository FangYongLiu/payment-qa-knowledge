---
id: tbl_cmf_tt_pos_batch
object_type: Table
name: POS批次表 (tt_pos_batch)
aliases: [tt_pos_batch, cmf.tt_pos_batch]
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

# POS批次表 (tt_pos_batch)

## 用途
物理表 `cmf.tt_pos_batch`,主键 `BATCH_ID`。POS批次表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `BATCH_ID` | decimal(11) | 批次ID |
| `TERMINAL_ID` | decimal(5) | 终端ID |
| `INST_BATCH_NO` | varchar(32) | 机构批次号 · 可空 |
| `STATUS` | char | 状态。I：初始；P：使用中；S：结算成功；F：结算失败； |
| `WORK_KEY` | varchar(256) | 工作密钥 · 可空 |
| `CHECK_IN_INST_NO` | varchar(32) | 签到机构订单号 · 可空 |
| `GMT_CHECK_IN` | timestamp | 签到时间 · 可空 |
| `CHECK_OUT_INST_NO` | varchar(32) | 签退机构订单号 · 可空 |
| `GMT_CHECK_OUT` | timestamp | 签退时间 · 可空 |
| `GMT_BOOKING_SETTLE` | timestamp | 预计结算时间 · 可空 |
| `GMT_SETTLE` | timestamp | 结算时间 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`BATCH_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
