---
id: tbl_basicrcdata_tm_member_identity
object_type: Table
name: 会员标识表,源表为支付：pmd实例，member库的tm_member_identity (tm_member_identity)
aliases: [tm_member_identity, basicrcdata.tm_member_identity]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basicrcdata schema DDL
tags: [risk, basicrcdata]
sensitivity: normal
related_services: []
---

# 会员标识表,源表为支付：pmd实例，member库的tm_member_identity (tm_member_identity)

## 用途
物理表 `basicrcdata.tm_member_identity`,主键 `IDENTITY, pid`。会员标识表,源表为支付：pmd实例，member库的tm_member_identity。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `MEMBER_ID` | varchar(32) | 会员编号 |
| `IDENTITY` | varchar(50) | 会员标识 |
| `STATUS` | decimal(8) | 1：有效；0：无效 |
| `IS_RECV_ADDR` | decimal(8) | 1：可以作为收款标识；0：不可以作为收款标识 |
| `IDENTITY_TYPE` | decimal(8) | 标识类型（0：uid 1：邮箱 2:手机） |
| `CREATE_TIME` | timestamp | 创建时间 |
| `UPDATE_TIME` | timestamp | 修改时间 · 可空 |
| `MEMO` | varchar(255) | 备注 · 可空 |
| `pid` | decimal(8) | 平台类型 |

## 主键 / 索引
- 主键:`IDENTITY, pid`
- `IDX_IDENTITY_MEMBER_ID`:MEMBER_ID

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
