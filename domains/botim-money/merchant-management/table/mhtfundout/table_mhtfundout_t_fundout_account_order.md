---
id: tbl_mhtfundout_t_fundout_account_order
object_type: Table
name: 转账到账号订单 (t_fundout_account_order)
aliases: [t_fundout_account_order, mhtfundout.t_fundout_account_order]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mhtfundout schema DDL
tags: [merchant-management, mhtfundout]
sensitivity: normal
related_services: []
---

# 转账到账号订单 (t_fundout_account_order)

## 用途
物理表 `mhtfundout.t_fundout_account_order`,主键 `global_id`。转账到账号订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局号 |
| `beneficiary_id` | bigint | 受益人id |

## 主键 / 索引
- 主键:`global_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
