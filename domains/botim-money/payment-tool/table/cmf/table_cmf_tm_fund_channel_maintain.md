---
id: tbl_cmf_tm_fund_channel_maintain
object_type: Table
name: 维护期 (tm_fund_channel_maintain)
aliases: [tm_fund_channel_maintain, cmf.tm_fund_channel_maintain]
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

# 维护期 (tm_fund_channel_maintain)

## 用途
物理表 `cmf.tm_fund_channel_maintain`,主键 `MAINTAIN_ID`。维护期。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `MAINTAIN_ID` | int unsigned | 维护ID · 可空 |
| `FUND_CHANNEL_CODE` | varchar(32) | 资金源编码 · 可空 |
| `FUND_CHANNEL_API` | varchar(48) | 资金渠道接口 · 可空 |
| `DESCRIPTION` | varchar(128) | 描述 · 可空 |
| `MAINTAIN_CONTENT` | varchar(1024) | 维护公告 · 可空 |
| `GMT_BEGIN` | timestamp | 维护开始时间 |
| `GMT_END` | timestamp | 维护结束时间 |
| `FUND_CHANNEL_BACKUP` | varchar(32) | 备用资金源 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `TARGET_INST_CODE` | varchar(16) | 目标机构码 · 可空 |

## 主键 / 索引
- 主键:`MAINTAIN_ID`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
