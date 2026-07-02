---
id: tbl_contract_t_contract_content_param
object_type: Table
name: 协议信息扩展表 (t_contract_content_param)
aliases: [t_contract_content_param, contract.t_contract_content_param]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: contract schema DDL
tags: [merchant-management, contract]
sensitivity: normal
related_services: []
---

# 协议信息扩展表 (t_contract_content_param)

## 用途
物理表 `contract.t_contract_content_param`,主键 `id, pkey`。协议信息扩展表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `contract_no` | bigint | 协议编号 |
| `pkey` | varchar(200) | 参数键 |
| `value` | varchar(200) | 参数值 |

## 主键 / 索引
- 主键:`id, pkey`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
