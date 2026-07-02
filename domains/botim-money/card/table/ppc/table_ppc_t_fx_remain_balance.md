---
id: tbl_ppc_t_fx_remain_balance
object_type: Table
name: Foreign Exchange Remain Balance (t_fx_remain_balance)
aliases: [t_fx_remain_balance, ppc.t_fx_remain_balance]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppc schema DDL
tags: [card, ppc]
sensitivity: normal
related_services: []
---

# Foreign Exchange Remain Balance (t_fx_remain_balance)

## 用途
物理表 `ppc.t_fx_remain_balance`,主键 `currency_code`。Foreign Exchange Remain Balance。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `currency_code` | char(3) | Currency Code |
| `selling_amount` | decimal(19, 4) | Selling Amount |
| `hold_amount` | decimal(19, 4) | Hold Amount |
| `version` | bigint | Version |
| `create_time` | timestamp(3) | Create time |
| `update_time` | timestamp(3) | Update time |

## 主键 / 索引
- 主键:`currency_code`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
