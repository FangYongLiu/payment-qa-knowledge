---
id: tbl_cmf_tl_inst_communicate
object_type: Table
name: 渠道补单信息 (tl_inst_communicate)
aliases: [tl_inst_communicate, cmf.tl_inst_communicate]
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

# 渠道补单信息 (tl_inst_communicate)

## 用途
物理表 `cmf.tl_inst_communicate`,主键 `COMMUNICATE_ID`。渠道补单信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `COMMUNICATE_ID` | decimal(11) | 通讯ID |
| `FUND_CHANNEL_CODE` | varchar(16) | 资金渠道代码 |
| `API_CODE` | varchar(16) | API代码 · 可空 |
| `GMT_LAST_PROCESS` | timestamp | 最后处理时间 · 可空 |

## 主键 / 索引
- 主键:`COMMUNICATE_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
