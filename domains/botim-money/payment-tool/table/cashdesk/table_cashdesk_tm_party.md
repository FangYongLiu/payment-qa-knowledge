---
id: tbl_cashdesk_tm_party
object_type: Table
name: 策略参与方 (tm_party)
aliases: [tm_party, cashdesk.tm_party]
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

# 策略参与方 (tm_party)

## 用途
物理表 `cashdesk.tm_party`,主键 `PARTY_ID`。策略参与方。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `PARTY_ID` | bigint(10) | 参与方ID · 可空 |
| `GROUP_ID` | decimal | 分组ID |
| `MEMBER_ID` | varchar(100) | 参与方会员ID · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`PARTY_ID`
- `UK_GROUP_ID_MEMBER_ID`:MEMBER_ID, GROUP_ID (UNIQUE)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
