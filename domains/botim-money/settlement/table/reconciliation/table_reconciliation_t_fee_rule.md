---
id: tbl_reconciliation_t_fee_rule
object_type: Table
name: 渠道手续费规则表 渠道手续费规则,记录规则 (t_fee_rule)
aliases: [t_fee_rule, reconciliation.t_fee_rule]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# 渠道手续费规则表 渠道手续费规则,记录规则 (t_fee_rule)

## 用途
物理表 `reconciliation.t_fee_rule`,主键 `fee_id`。渠道手续费规则表 渠道手续费规则,记录规则。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `fee_id` | bigint | 规则ID |
| `fund_channel_code` | varchar(32) | 渠道编号 · 可空 |
| `biz_type` | varchar(3) | 业务类型 · 可空 |
| `fee_type` | varchar(4) | 手续费类型 F:手续费 V:增值税 · 可空 |
| `rule_type` | varchar(4) | 规则类型 S:单笔收费 P:单笔百分比收费 · 可空 |
| `regulation` | varchar(128) | 手续费规则 根据规则类型计算 eg: 0.15 = 单笔收费0.15 或 单笔收费15% · 可空 |
| `memo` | varchar(256) | 备注 · 可空 |
| `status` | varchar(4) | 状态 是否启用,手续费规则禁用后产生的入账流水费用默认为零 Y:启用 N:禁用 · 可空 |
| `inure_time` | timestamp | 生效时间 生效时间,配置或修改手续费规则后可指定生效时间。默认为立即生效 · 可空 |
| `Invalid_time` | timestamp | 失效时间 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`fee_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
