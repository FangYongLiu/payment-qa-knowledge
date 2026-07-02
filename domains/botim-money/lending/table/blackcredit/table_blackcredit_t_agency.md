---
id: tbl_blackcredit_t_agency
object_type: Table
name: 代理 (t_agency)
aliases: [t_agency, blackcredit.t_agency]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: blackcredit schema DDL
tags: [lending, blackcredit]
sensitivity: normal
related_services: []
---

# 代理 (t_agency)

## 用途
物理表 `blackcredit.t_agency`,主键 `mid`。代理。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `mid` | varchar(32) | 会员id |
| `name` | varchar(100) | 名字 |
| `status` | varchar(32) | 代理状态 |
| `notify_state` | varchar(32) | 收单状态 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`mid`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
