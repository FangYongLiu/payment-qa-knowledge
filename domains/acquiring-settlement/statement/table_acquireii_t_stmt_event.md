---
id: tbl_acquireii_t_stmt_event
object_type: Table
domain: acquiring-settlement
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_stmt_event.md
tags:
- statement
- settlement
- event
subdomain: statement
module: null
sensitivity: normal
name: 对账事件表 (t_stmt_event)
aliases:
- t_stmt_event
- acquireii.t_stmt_event
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
记录收单订单的**对账（statement）事件**。statement = 财务对账，是收单业务的关键环节。

典型场景：
- T+1 商户对账：用户扫码支付 100 AED，T+1 商户收到结算款
- 系统生成对账事件，通知财务、商户后台、统计系统
- 对账事件驱动下游系统（财务、报表、风控等）更新数据

表名：`acquireii.t_stmt_event`，表注释 `stmt event`，重要程度 ⭐⭐⭐⭐。

## 关键列
**主键和事件信息**
- `id` bigint 主键，事件 ID
- `event_id` varchar(200) 事件标识
- `event_type` varchar(64) 事件类型（可能有 ACQUIRE_SETTLE / REFUND_SETTLE / VOID_SETTLE 等）

**业务方**
- `partner_id` varchar(64) 商户 ID

**时间和版本**
- `created_time` timestamp(3) 创建时间
- `last_updated_time` timestamp(3) 最后更新时间
- `data_version` bigint 数据版本

## 主键/索引
| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | id | 主键 |
| `i_se_eid` | event_id | 按 event_id 查 |
| `i_se_ct` | created_time | 按时间查 |

**关联表**：
- `t_event_param`：1:N，关联字段 `id`（事件参数：金额、币种等明细）
- `t_acquire_order`：通过 `event_id` 间接关联

## 校验点(QA 关注)
1. **event_type 区分对账类型**：需校验 ACQUIRE_SETTLE / REFUND_SETTLE / VOID_SETTLE 等类型分发是否正确
2. **不一定每笔交易都生成 event**：可能按批次生成，验证时不要假设 1:1 对应
3. **下游系统订阅**：财务、报表、风控等系统消费此事件，需关注事件投递与幂等
4. **事件参数在 `t_event_param`**：金额、币种等明细需联表查询
5. 常用查询路径：按 `event_id` 查、按 `partner_id + DATE(created_time)` 聚合 event_type 统计、`t_stmt_event LEFT JOIN t_event_param ON se.id = ep.id` 查完整事件信息
