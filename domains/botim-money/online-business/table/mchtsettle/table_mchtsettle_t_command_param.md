---
id: tbl_mchtsettle_t_command_param
object_type: Table
name: 指令参数表 (t_command_param)
aliases: [t_command_param, mchtsettle.t_command_param]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mchtsettle schema DDL
tags: [online-business, 商户结算, mchtsettle]
sensitivity: normal
related_services: [svc_merchant_settlement]
---

# 指令参数表 (t_command_param)

## 用途
物理表 `mchtsettle.t_command_param`,主键 `id, pkey`。command param。属商户结算服务 [[svc_merchant_settlement]]。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:[[svc_merchant_settlement]](= `related_services`)。
- **谁读写它**:结算链路的服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | command id |
| `pkey` | varchar(50) | param key |
| `value` | varchar(200) | param value |

## 主键 / 索引
- 主键:`id, pkey`
- 无(仅主键)

## 校验点(QA 关注)
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
