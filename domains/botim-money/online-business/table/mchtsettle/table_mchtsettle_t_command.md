---
id: tbl_mchtsettle_t_command
object_type: Table
name: 指令表 (t_command)
aliases: [t_command, mchtsettle.t_command]
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

# 指令表 (t_command)

## 用途
物理表 `mchtsettle.t_command`,主键 `id`。command。属商户结算服务 [[svc_merchant_settlement]]。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:[[svc_merchant_settlement]](= `related_services`)。
- **谁读写它**:结算链路的服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `category` | varchar(50) | command type |
| `external_order_id` | varchar(100) | outer order id · 可空 |
| `status` | varchar(12) | status · 可空 |
| `memo` | varchar(100) | memo · 可空 |
| `created_time` | timestamp | created_time |
| `last_updated_time` | timestamp | last_updated_time |
| `data_version` | bigint | data version |

## 主键 / 索引
- 主键:`id`
- `i_cmd_eoi`:external_order_id
- `i_urcmd_ct`:created_time

## 校验点(QA 关注)
- **时间字段**:`created_time`=入库、`last_updated_time`=最后更新;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发场景校验版本递增。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
