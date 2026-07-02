---
id: tbl_ccdpm_t_dpm_buffer_rule
object_type: Table
name: 缓冲入账规则表 (t_dpm_buffer_rule)
aliases: [t_dpm_buffer_rule, ccdpm.t_dpm_buffer_rule]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccdpm schema DDL
tags: [crypto, ccdpm]
sensitivity: normal
related_services: []
---

# 缓冲入账规则表 (t_dpm_buffer_rule)

## 用途
物理表 `ccdpm.t_dpm_buffer_rule`,主键 `buffer_rule_id`。缓冲入账规则表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `buffer_rule_id` | bigint | 缓冲规则ID |
| `product_code` | varchar(12) | 产品编码 |
| `pay_code` | varchar(12) | PE支付编码 |
| `account_no` | varchar(32) | 账户号 · 可空 |
| `status` | decimal(1) | 状态：0:有效,1:无效(已删除) |
| `crdr` | decimal(1) | 借贷标志：0:双向,1:借,2:贷 |
| `remark` | varchar(256) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `valid_time` | timestamp | 生效时间 |
| `unvalid_time` | timestamp | 失效时间 |

## 主键 / 索引
- 主键:`buffer_rule_id`
- `uk_biz_key`:product_code, pay_code, account_no, crdr (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
