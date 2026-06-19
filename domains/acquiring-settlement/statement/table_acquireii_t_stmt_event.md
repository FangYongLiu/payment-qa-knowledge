---
id: tbl_acquireii_t_stmt_event
object_type: Table
domain: acquire-transaction
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
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_amount_detail
- tbl_acquireii_t_event_param
- tbl_acquireii_t_payment_info
- tbl_acquireii_t_refund_order
- tbl_acquireii_t_void_order
related_scenarios:
- scn_acquire_product_apply
- scn_merchant_transaction_db_check
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
记录收单订单的**对账（statement）事件**。statement = 财务对账，是收单业务的关键环节，也是收单交易链路在 T+1 之后向下游（财务、商户后台、报表、风控等）输出的事实来源。

典型场景：
- T+1 商户对账：用户扫码支付 100 AED，T+1 商户收到结算款
- 系统生成对账事件，通知财务、商户后台、统计系统
- 对账事件驱动下游系统（财务、报表、风控等）更新数据

表名：`acquireii.t_stmt_event`，表注释 `stmt event`，重要程度 ⭐⭐⭐⭐。

## 在交易链路中的位置
```
[支付/退款/撤销完成]
    ├─ t_acquire_order / t_refund_order / t_void_order  （订单态终态）
    │       │
    │       ▼
    │   [对账批次/结算]
    │       │
    └─►  t_stmt_event  ── 1:N ──►  t_event_param  （事件明细：金额、币种等）
            │
            ▼
        下游订阅：财务系统 / 商户后台 / 报表 / 风控
```
对账事件位于交易链路的**末端事实层**，不参与实时交易决策，仅承载结算/对账语义，由批处理或交易终态触发产生。

## 关键列
**主键和事件信息**
- `id` bigint 主键，事件 ID（同时用于关联 `t_event_param.id`）
- `event_id` varchar(200) 事件标识（业务幂等键，下游订阅按此去重）
- `event_type` varchar(64) 事件类型（如 ACQUIRE_SETTLE / REFUND_SETTLE / VOID_SETTLE 等）

**业务方**
- `partner_id` varchar(64) 商户 ID

**时间和版本**
- `created_time` timestamp(3) 创建时间
- `last_updated_time` timestamp(3) 最后更新时间
- `data_version` bigint 数据版本（乐观锁）

## 主键 / 索引
| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | id | 主键 |
| `i_se_eid` | event_id | 按 event_id 查事件 |
| `i_se_ct` | created_time | 按时间范围查/对账日切 |

## 关联表
| 关联表 | 关系 | 关联字段 | 说明 |
|--------|------|----------|------|
| `t_event_param` | 1:N | `t_stmt_event.id = t_event_param.id` | 事件参数明细：金额、币种、订单号等 |
| `t_acquire_order` | 间接 | 通过 `event_id` 或参数中的 order_no | 关联原始收单订单 |
| `t_refund_order` | 间接 | 通过事件参数 | REFUND_SETTLE 类型对应退款订单 |
| `t_void_order` | 间接 | 通过事件参数 | VOID_SETTLE 类型对应撤销订单 |
| `t_payment_info` / `t_amount_detail` | 间接 | 通过订单号 | 校验对账金额与原交易金额一致 |

## 校验点（QA 关注）
1. **event_type 区分对账类型**：需校验 ACQUIRE_SETTLE / REFUND_SETTLE / VOID_SETTLE 等类型分发是否正确，类型不能与原始订单类型错配（例如退款单只能产 REFUND_SETTLE）。
2. **不一定每笔交易都生成 event**：可能按批次生成，验证时不要假设 1:1 对应；应按 `partner_id + DATE(created_time) + event_type` 维度聚合校验。
3. **下游系统订阅**：财务、报表、风控等系统消费此事件，需关注事件投递与幂等（以 `event_id` 为幂等键）。
4. **事件参数在 `t_event_param`**：金额、币种等明细需联表查询，单看本表无法判断金额正确性。
5. **金额一致性**：与 `t_acquire_order` / `t_refund_order` / `t_amount_detail` 的金额、币种、商户号需对得上。
6. **常用查询路径**：
   - 按 `event_id` 精确查：`SELECT * FROM t_stmt_event WHERE event_id = ?`
   - 按商户日聚合：`SELECT event_type, COUNT(*) FROM t_stmt_event WHERE partner_id=? AND DATE(created_time)=? GROUP BY event_type`
   - 联参数表查完整事件：`SELECT se.*, ep.* FROM t_stmt_event se LEFT JOIN t_event_param ep ON se.id = ep.id WHERE se.event_id = ?`
