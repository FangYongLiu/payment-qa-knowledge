---
id: tbl_personal_t_check_config
object_type: Table
name: 校验配置表 (t_check_config)
aliases: [t_check_config, personal.t_check_config]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: personal schema DDL
tags: [activation, personal]
sensitivity: normal
related_services: []
---

# 校验配置表 (t_check_config)

## 用途
物理表 `personal.t_check_config`,主键 `id`。校验配置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `type` | varchar(25) | 类型，例如：BEFORE - 前置校验 |
| `sub_type` | varchar(25) | 子类型,例如：WITHDRAW - 提现，ACCOUNT_TRANSFER - 好友转账 |
| `level` | varchar(20) | 校验级别,例如：LEVEL_1 - 强制，LEVEL_2 - 提示 |
| `element` | varchar(150) | 校验元素,例如:SVA[EID,PASSPORT] |
| `routing_key` | varchar(150) | 路由key · 可空 |
| `tips_key` | varchar(150) | 提示，国际化key · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `uk_ck_config_key_t_sub_type`:type, sub_type (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
