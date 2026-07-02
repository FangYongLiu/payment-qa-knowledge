---
id: tbl_ons_t_notify_match_config
object_type: Table
name: 平台匹配规则 (t_notify_match_config)
aliases: [t_notify_match_config, ons.t_notify_match_config]
domain: infrastructure
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ons schema DDL
tags: [infrastructure, ons]
sensitivity: normal
related_services: []
---

# 平台匹配规则 (t_notify_match_config)

## 用途
物理表 `ons.t_notify_match_config`,主键 `id`。平台匹配规则。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | id · 可空 |
| `biz_product_code` | varchar(32) | 业务产品码：业务产品码 |
| `role` | varchar(32) | 角色：角色 |
| `payment_type` | varchar(32) | 支付类型：pay,refund |
| `status` | varchar(32) | 账单状态：账单状态 |
| `notify_strategy` | varchar(32) | 通知策略 · 可空 |
| `rule_code` | varchar(32) | 规则Code：发送平台规则 |
| `event_code` | varchar(32) | 通知类型：通知类型 |
| `enable_flag` | char | 启用标识：Y=启用，N=停用 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `uk_product_role_payment_event`:biz_product_code, role, payment_type, event_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
