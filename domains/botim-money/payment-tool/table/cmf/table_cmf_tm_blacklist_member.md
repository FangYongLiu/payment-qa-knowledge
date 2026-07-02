---
id: tbl_cmf_tm_blacklist_member
object_type: Table
name: tm_blacklist_member (tm_blacklist_member)
aliases: [tm_blacklist_member, cmf.tm_blacklist_member]
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

# tm_blacklist_member (tm_blacklist_member)

## 用途
物理表 `cmf.tm_blacklist_member`,主键 `PT_ID`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `PT_ID` | varchar(32) | 会员ID |
| `GMT_CREATE` | timestamp | 创建时间 · 可空 |

## 主键 / 索引
- 主键:`PT_ID`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
