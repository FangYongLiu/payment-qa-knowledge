---
id: tbl_point_t_account
object_type: Table
name: 账户 (t_account)
aliases: [t_account, point.t_account]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: point schema DDL
tags: [marketing, point]
sensitivity: normal
related_services: []
---

# 账户 (t_account)

## 用途
物理表 `point.t_account`,主键 `account_no`。账户。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `account_no` | bigint | 账户号：前八后九 |
| `member_id` | varchar(32) | 会员号 |
| `point_type` | varchar(10) | 点数类型 |
| `available_amount` | decimal(19, 4) | 可用数量 |
| `frozen_amount` | decimal(19, 4) | 冻结数量 |
| `to_expire_available_amount` | decimal(19, 4) | 待失效可用数量 |
| `to_expire_frozen_amount` | decimal(19, 4) | 待失效冻结数量 |
| `to_expire_time` | timestamp | 待失效时间 · 可空 |
| `accounting_version` | bigint | 记账版本 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`account_no`
- `uk_member_id_point_type`:member_id, point_type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
