---
id: tbl_acquireii_t_stmt_event
object_type: Table
name: 对账事件表 (t_stmt_event)
aliases: [t_stmt_event, acquireii.t_stmt_event]
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

# 对账事件表 (t_stmt_event)

## 用途
物理表 `acquireii.t_stmt_event`,主键 `id`。对账事件。属收单服务 [[svc_acquireii]]。业务语义细节**待补**(表结构来自 DDL,用途需结合代码/文档补充)。

## 关联关系
- **所属服务**:[[svc_acquireii]](= `related_services`)。
- **谁读写它**:收单链路的服务 / 接口(由对方文档的 `related_tables` 声明,本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 事件id |
| `transaction_type` | varchar(32) | 事件类型 |
| `stmt_type` | varchar(32) | 对账单类型 |
| `order_type` | varchar(16) | 任务类型 |
| `order_id` | bigint | 对象id |
| `created_time` | timestamp(3) | 创建时间 |

## 主键 / 索引
- 主键:`id`
- `i_evt_ct`:created_time
- `i_evt_order`:order_type, order_id

## 校验点(QA 关注)
- **时间字段**:`created_time`=入库、`last_updated_time`=最后更新;按时间过滤走对应索引,勿混用。
- **关联订单**:`order_id` 关联收单/退款主单(结合 `order_type` 判断单据类型)。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
