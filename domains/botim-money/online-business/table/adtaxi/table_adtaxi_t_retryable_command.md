---
id: tbl_adtaxi_t_retryable_command
object_type: Table
name: 可重试指令表 (t_retryable_command)
aliases: [t_retryable_command, adtaxi.t_retryable_command]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: adtaxi schema DDL
tags: [online-business, 出租车支付, adtaxi]
sensitivity: normal
related_services: [svc_adtaxi]
---

# 可重试指令表 (t_retryable_command)

## 用途
物理表 `adtaxi.t_retryable_command`,主键 `id`。可重试指令(分区)。属出租车支付服务 [[svc_adtaxi]]。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:[[svc_adtaxi]](= `related_services`)。
- **谁读写它**:出租车支付链路的服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `parent_type` | varchar(50) | 订单类型 |
| `parent_id` | bigint | 订单id |
| `command` | varchar(50) | 指令 |

## 主键 / 索引
- 主键:`id`
- `i_rcmd_prt`:parent_id, parent_type, command

## 校验点(QA 关注)
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
