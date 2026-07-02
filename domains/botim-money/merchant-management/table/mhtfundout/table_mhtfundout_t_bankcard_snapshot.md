---
id: tbl_mhtfundout_t_bankcard_snapshot
object_type: Table
name: 银行卡快照 (t_bankcard_snapshot)
aliases: [t_bankcard_snapshot, mhtfundout.t_bankcard_snapshot]
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

# 银行卡快照 (t_bankcard_snapshot)

## 用途
物理表 `mhtfundout.t_bankcard_snapshot`,主键 `global_id`。银行卡快照。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局号 |
| `bank_name` | varchar(100) | 银行名称 · 可空 |
| `location` | varchar(50) | 银行卡开户国家 · 可空 |
| `account_num_mask` | varchar(50) | 银行卡号掩码 · 可空 |
| `account_name` | varchar(100) | 账号名称 · 可空 |
| `swift_code` | varchar(50) | swift Code · 可空 |

## 主键 / 索引
- 主键:`global_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
