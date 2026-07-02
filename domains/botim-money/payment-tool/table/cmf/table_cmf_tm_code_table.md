---
id: tbl_cmf_tm_code_table
object_type: Table
name: tm_code_table (tm_code_table)
aliases: [tm_code_table, cmf.tm_code_table]
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

# tm_code_table (tm_code_table)

## 用途
物理表 `cmf.tm_code_table`,主键 `CODE_ID`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CODE_ID` | decimal(8) | 字典ID |
| `CODE_KEY` | varchar(32) | 字典标识 |
| `ATTR_NAME` | varchar(32) | 属性名称 · 可空 |
| `ATTR_KEY` | varchar(32) | 属性标识 |
| `ATTR_VALUE` | varchar(32) | 属性值 · 可空 |
| `ENABLE` | char | 是否使用 · 可空 |

## 主键 / 索引
- 主键:`CODE_ID`
- `IX_CODETABLE_CODEKEY_ATTRKEY`:CODE_KEY, ATTR_KEY (UNIQUE)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
