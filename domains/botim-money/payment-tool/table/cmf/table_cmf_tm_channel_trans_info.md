---
id: tbl_cmf_tm_channel_trans_info
object_type: Table
name: 渠道交易需要用到的特定信息 (tm_channel_trans_info)
aliases: [tm_channel_trans_info, cmf.tm_channel_trans_info]
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

# 渠道交易需要用到的特定信息 (tm_channel_trans_info)

## 用途
物理表 `cmf.tm_channel_trans_info`,主键 `TRANS_ID`。渠道交易需要用到的特定信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `TRANS_ID` | int unsigned | 主键id · 可空 |
| `FUND_CHANNEL_CODE` | varchar(32) | 资金渠道编码 · 可空 |
| `API_TYPE` | varchar(16) | api类型 · 可空 |
| `TRANS_CODE` | varchar(16) | 交易代码 · 可空 |
| `STATUS` | char | 状态 · 可空 |
| `EXTENSION` | varchar(512) | 扩展信息 · 可空 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |

## 主键 / 索引
- 主键:`TRANS_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
