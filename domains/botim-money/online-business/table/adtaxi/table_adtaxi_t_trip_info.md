---
id: tbl_adtaxi_t_trip_info
object_type: Table
name: 行程信息表 (t_trip_info)
aliases: [t_trip_info, adtaxi.t_trip_info]
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

# 行程信息表 (t_trip_info)

## 用途
物理表 `adtaxi.t_trip_info`,主键 `id`。行程信息。属出租车支付服务 [[svc_adtaxi]]。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:[[svc_adtaxi]](= `related_services`)。
- **谁读写它**:出租车支付链路的服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `driver_id` | varchar(32) | 驾驶员ID · 可空 |
| `driver_name` | varchar(128) | 驾驶员姓名 · 可空 |
| `mobile_no` | varchar(32) | 待补 · 可空 |
| `franchise` | varchar(64) | franchise · 可空 |
| `taxi_no` | varchar(32) | 出租车NO · 可空 |
| `taxi_type` | varchar(32) | 出租车类型 · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_td_str`:franchise
- `i_td_t`:driver_name

## 校验点(QA 关注)
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
