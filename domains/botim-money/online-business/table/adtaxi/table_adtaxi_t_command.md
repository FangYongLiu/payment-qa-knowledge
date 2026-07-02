---
id: tbl_adtaxi_t_command
object_type: Table
name: 指令表 (t_command)
aliases: [t_command, adtaxi.t_command]
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

# 指令表 (t_command)

## 用途
物理表 `adtaxi.t_command`,主键 `id`。所有的发出id都从这里读。属出租车支付服务 [[svc_adtaxi]]。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:[[svc_adtaxi]](= `related_services`)。
- **谁读写它**:出租车支付链路的服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `category` | varchar(50) | 命令类型 |
| `external_order_id` | varchar(100) | 外部订单id · 可空 |
| `status` | varchar(50) | 状态 · 可空 |
| `memo` | varchar(100) | 备注 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `last_updated_time` | timestamp | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `i_urcmd_ct`:created_time

## 校验点(QA 关注)
- **时间字段**:`created_time`=入库、`last_updated_time`=最后更新;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发场景校验版本递增。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
