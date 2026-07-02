---
id: tbl_gpoint_t_buffer_rule
object_type: Table
name: 缓冲规则 (t_buffer_rule)
aliases: [t_buffer_rule, gpoint.t_buffer_rule]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: gpoint schema DDL
tags: [marketing, gpoint]
sensitivity: normal
related_services: []
---

# 缓冲规则 (t_buffer_rule)

## 用途
物理表 `gpoint.t_buffer_rule`,主键 `rule_id`。缓冲规则。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `rule_id` | bigint | 规则ID · 可空 |
| `account_type` | varchar(10) | 账户类型 |
| `account_identity` | varchar(32) | 账户标志：*表示全匹配 |
| `accounting_type` | varchar(10) | 记账类型：*表示全匹配 |
| `biz_product_code` | varchar(10) | 业务产品码：*表示全匹配 |
| `clearing_code` | varchar(64) | 清算编码：*表示全匹配 |
| `enable_flag` | char | 启用标识：Y=启用，N=停用 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`rule_id`
- `idx_account_type_identity`:account_type, account_identity

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
