---
id: tbl_cashdesk_tr_filter_party_group
object_type: Table
name: 参与方组策略关系 (tr_filter_party_group)
aliases: [tr_filter_party_group, cashdesk.tr_filter_party_group]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cashdesk schema DDL
tags: [payment-tool, cashdesk]
sensitivity: normal
related_services: []
---

# 参与方组策略关系 (tr_filter_party_group)

## 用途
物理表 `cashdesk.tr_filter_party_group`,主键 `GROUP_FILTER_ID`。参与方组策略关系。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `GROUP_FILTER_ID` | decimal | 关联关系id,初始信息手动配置 |
| `FILTER_ID` | decimal | 过滤策略ID |
| `GROUP_ID` | decimal | 分组ID |
| `GMT_CREATE` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`GROUP_FILTER_ID`
- `UK_PARTY_GROUP_FILTER`:FILTER_ID, GROUP_ID (UNIQUE)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
