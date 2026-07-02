---
id: tbl_reconciliation_t_fee_account_info
object_type: Table
name: t_fee_account_info (t_fee_account_info)
aliases: [t_fee_account_info, reconciliation.t_fee_account_info]
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

# t_fee_account_info (t_fee_account_info)

## 用途
物理表 `reconciliation.t_fee_account_info`,主键 `flow_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `flow_id` | int | 主键 · 可空 |
| `fund_channel_code` | varchar(32) | 渠道编号 · 可空 |
| `biz_type` | varchar(8) | 业务类型 · 可空 |
| `account_type` | varchar(8) | 账户类型CV-增值税结转 CF手续费结转 · 可空 |
| `cr_account_no` | varchar(64) | Credit账号 · 可空 |
| `dr_account_no` | varchar(64) | Debit账号 · 可空 |
| `status` | varchar(4) | 启用、停用 · 可空 |
| `round_type` | varchar(8) | 四舍五入类型，R-四舍五入，D-舍弃余数，U-进一法 · 可空 |
| `round_precision` | varchar(4) | 保留几位小数 最多8位 · 可空 |
| `tax_rate` | varchar(8) | 税率 小数点 eg:16%税率 此处填写0.16 · 可空 |
| `tax_rate_priority` | varchar(4) | 税率优先级，四舍五入和税率的优先级 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `operator` | varchar(32) | 创建者 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`flow_id`
- `uk_channel_account_type`:fund_channel_code, biz_type, account_type (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
