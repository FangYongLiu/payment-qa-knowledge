---
id: tbl_cmf_tt_ext_clob
object_type: Table
name: 大数据扩展表 (tt_ext_clob)
aliases: [tt_ext_clob, cmf.tt_ext_clob]
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

# 大数据扩展表 (tt_ext_clob)

## 用途
物理表 `cmf.tt_ext_clob`,主键 `EXT_ID`。大数据扩展表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `EXT_ID` | decimal(11) | 扩展ID |
| `RELATED_ID` | decimal(15) | 关联ID |
| `RELATED_TYPE` | varchar(16) | 关联类型 |
| `ATTR_KEY` | varchar(32) | 属性名 |
| `ATTR_VALUE` | text | 属性值 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`EXT_ID`
- `I_TT_EXT_CLOB_RELATED_ID`:RELATED_ID

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
