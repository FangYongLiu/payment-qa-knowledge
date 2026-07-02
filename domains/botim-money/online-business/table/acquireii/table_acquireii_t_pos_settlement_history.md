---
id: tbl_acquireii_t_pos_settlement_history
object_type: Table
name: POS 结算历史表 (t_pos_settlement_history)
aliases: [t_pos_settlement_history, acquireii.t_pos_settlement_history]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: acquireii schema DDL
tags: [online-business, 收单, acquireii]
sensitivity: normal
related_services: [svc_acquireii]
---

# POS 结算历史表 (t_pos_settlement_history)

## 用途
物理表 `acquireii.t_pos_settlement_history`,主键 `id`。pos_settlement history record。属收单服务 [[svc_acquireii]]。业务语义细节**待补**(表结构来自 DDL,用途需结合代码/文档补充)。

## 关联关系
- **所属服务**:[[svc_acquireii]](= `related_services`)。
- **谁读写它**:收单链路的服务 / 接口(由对方文档的 `related_tables` 声明,本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id primary key |
| `device_id` | varchar(32) | device id |
| `partner_id` | varchar(32) | memberId |
| `start_time` | timestamp(3) | start time |
| `end_time` | timestamp(3) | end time |
| `operator_id` | varchar(50) | operator id |
| `created_time` | timestamp(3) | created time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:`created_time`=入库、`last_updated_time`=最后更新;按时间过滤走对应索引,勿混用。
- **device 维度**:按 `device_id` 组织的批次/结算通常唯一,注意重复校验。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
