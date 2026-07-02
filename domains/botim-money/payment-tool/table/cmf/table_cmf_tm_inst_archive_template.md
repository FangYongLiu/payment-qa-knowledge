---
id: tbl_cmf_tm_inst_archive_template
object_type: Table
name: 机构归档模板表 (tm_inst_archive_template)
aliases: [tm_inst_archive_template, cmf.tm_inst_archive_template]
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

# 机构归档模板表 (tm_inst_archive_template)

## 用途
物理表 `cmf.tm_inst_archive_template`,主键 `ARCHIVE_TEMPLATE_ID`。机构归档模板表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ARCHIVE_TEMPLATE_ID` | decimal(5) | 归档模板ID |
| `FUND_CHANNEL_API` | varchar(16) | 资金渠道API |
| `FUND_CHANNEL_CODE` | varchar(16) | 资金渠道编码 |
| `MAX_ITEM` | decimal | 最大笔数 |
| `MIN_ITEM` | decimal | 最小笔数 |
| `TIME_EXPRESSION` | varchar(64) | 时间表达式 |
| `CONDITION_EXPRESSION` | varchar(2048) | 条件表达式 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `ARCHIVE_TEMPLATE_KEY` | varchar(64) | 归档模板key 逻辑主键 · 可空 |
| `NEED_WORD_DATE` | char | 要求时间 · 可空 |
| `MAX_AMOUNT` | decimal(15, 2) | 最大金额 · 可空 |
| `API_NO_MODE_ID` | decimal(11) | 批次订单号生成规则 · 可空 |
| `ARCHIVE_BY_MERCHANT` | char | 按照商户归档,Y:是,N:否 · 可空 |

## 主键 / 索引
- 主键:`ARCHIVE_TEMPLATE_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
