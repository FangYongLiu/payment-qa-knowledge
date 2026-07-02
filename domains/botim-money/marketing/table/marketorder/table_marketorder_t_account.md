---
id: tbl_marketorder_t_account
object_type: Table
name: 缴费账户表 (t_account)
aliases: [t_account, marketorder.t_account]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketorder schema DDL
tags: [marketing, marketorder]
sensitivity: normal
related_services: []
---

# 缴费账户表 (t_account)

## 用途
物理表 `marketorder.t_account`,主键 `id`。缴费账户表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `member_id` | varchar(20) | 会员id |
| `account_type` | varchar(50) | 账户类型 |
| `biz_type` | varchar(20) | 业务类型 · 可空 |
| `account_number` | varchar(16) | 缴费户号 · 可空 |
| `service_provider` | varchar(20) | 服务机构 · 可空 |
| `package_type` | varchar(50) | 套餐类型：PrePaid：预付费 PostPaid：后付费 · 可空 |
| `account_aliases` | varchar(120) | 账户别名 · 可空 |
| `memo` | varchar(120) | 备注 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `country_code` | varchar(20) | 国家code · 可空 |
| `area_code` | varchar(12) | 区号 · 可空 |
| `currency` | varchar(12) | 币种 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_member_id`:member_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
