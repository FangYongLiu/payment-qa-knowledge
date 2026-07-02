---
id: tbl_cashdesk_tm_party_group
object_type: Table
name: 策略参与方分组 (tm_party_group)
aliases: [tm_party_group, cashdesk.tm_party_group]
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

# 策略参与方分组 (tm_party_group)

## 用途
物理表 `cashdesk.tm_party_group`,主键 `GROUP_ID`。策略参与方分组。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `GROUP_ID` | decimal | 分组ID,初始信息手动配置 |
| `GROUP_NAME` | varchar(64) | 分组名称 |
| `PARTY_ROLE` | varchar(36) | 参与方角色 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`GROUP_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
