---
id: tbl_router_t_channel_fee_rule
object_type: Table
name: 渠道手续费表 (t_channel_fee_rule)
aliases: [t_channel_fee_rule, router.t_channel_fee_rule]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: router schema DDL
tags: [payment-tool, router]
sensitivity: normal
related_services: []
---

# 渠道手续费表 (t_channel_fee_rule)

## 用途
物理表 `router.t_channel_fee_rule`,主键 `fee_id`。渠道手续费表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `fee_id` | int | id · 可空 |
| `channel_code` | varchar(32) | 渠道编号 · 可空 |
| `biz_type` | varchar(10) | 业务类型 · 可空 |
| `fee_type` | varchar(4) | 手续费类型 F:手续费 V:增值税 · 可空 |
| `rule_type` | varchar(4) | 规则类型 S:单笔收费 P:单笔百分比收费 · 可空 |
| `regulation` | varchar(128) | 手续费规则 根据规则类型计算 eg: 0.15 = 单笔收费0.15 或 单笔收费15% · 可空 |
| `round_type` | char | 四舍五入类型，R-四舍五入，D-舍弃余数，U-进一法 · 可空 |
| `precision` | smallint(5) | 保留几位小数 · 可空 |
| `fee_currency` | varchar(3) | 手续费币种 · 可空 |
| `memo` | varchar(256) | 备注 · 可空 |
| `enable` | char | 状态: Y-可用，N-不可用 · 可空 |
| `gmt_effect` | timestamp | 生效时间 · 可空 |
| `gmt_expired` | timestamp | 失效时间 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `extension` | varchar(255) | 扩展信息 · 可空 |
| `max_fee` | varchar(16) | max fee amount · 可空 |

## 主键 / 索引
- 主键:`fee_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
