---
id: tbl_reconciliation_t_accrual_config
object_type: Table
name: 计提配置表 (t_accrual_config)
aliases: [t_accrual_config, reconciliation.t_accrual_config]
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

# 计提配置表 (t_accrual_config)

## 用途
物理表 `reconciliation.t_accrual_config`,主键 `config_id`。计提配置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `config_id` | bigint | 配置id · 可空 |
| `source_type` | char(3) | 计提来源类型: FI:资金对账收入 CA:成本账号 TRV:手续费收入表 TRF:手续费退款表 |
| `accrual_type` | char | 计提类型: R:收入 C:支出 |
| `accrual_account` | varchar(32) | 计提账号 |
| `cost_title_code` | varchar(32) | 成本科目代码: 计提类型为C填写该字段 · 可空 |
| `revenue_accounts` | text | Revenue Account List · 可空 |
| `progress` | timestamp | 进度 · 可空 |
| `next_trigger_time` | timestamp | 下次触发时间 · 可空 |
| `enable_flag` | char | 是否启用: Y=Yes，N=No |
| `extension` | varchar(255) | 扩展信息 · 可空 |
| `memo` | varchar(100) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `write_off_account` | varchar(32) | 冲销账户 · 可空 |

## 主键 / 索引
- 主键:`config_id`
- `uk_source_type`:source_type (UNIQUE)
- `idx_trigger`:next_trigger_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
