---
id: tbl_acquireii_t_request_identity
object_type: Table
domain: acquire-order-system
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_request_identity.md
tags:
- 幂等
- 防重
- 请求标识
subdomain: null
module: null
sensitivity: normal
name: 请求标识表
aliases:
- t_request_identity
- acquireii.t_request_identity
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_deposit_order
- tbl_acquireii_t_refund_order
- tbl_acquireii_t_reversal_order
- tbl_acquireii_t_reversal_orderii
- tbl_acquireii_t_revoke_order
- tbl_acquireii_t_void_ops_order
- tbl_acquireii_t_void_order
related_scenarios:
- scn_acquire_product_apply
- scn_merchant_transaction_db_check
- scn_mit_autodebit
- scn_mit_cit_directpay_first
- scn_mit_cit_directpay_subsequent
- scn_mit_cit_payandsign
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_request_identity` 是收单系统**幂等防重的核心登记表**，负责为每个商户请求的 `request_no` 建立唯一身份标识，确保同一商户的相同请求不会产生两笔订单。它处于收单链路最前端，位于所有订单类业务（acquire/refund/void/reversal/revoke/deposit 等）落库**之前**，是入口处的幂等闸口。

## 在交易链路中的位置

```
商户请求 (request_no)
   │
   ▼
[t_request_identity]  ← 幂等查重 (issuer_type + issuer_code + request_no)
   │ 命中 → 返回已有 global_id（幂等返回原订单）
   │ 未命中 → 生成 global_id，登记本表
   ▼
订单主表（t_acquire_order / t_refund_order / t_void_order / t_reversal_order / t_revoke_order / t_deposit_order …）
   │
   ▼
后续指令、支付信息、对账事件等
```

**典型场景**：
- 商户调用 placeOrder 接口，传入 request_no = "ABC123"
- 系统先在 t_request_identity 查找 (issuer_type, issuer_code, request_no)
- 已存在 → 直接返回已有订单（幂等返回）
- 不存在 → 创建新订单并登记到本表

所有订单类业务（t_acquire_order / t_refund_order / t_void_order / t_reversal_order / t_revoke_order / t_deposit_order 等）都通过 `global_id` 与本表 **1:1 关联**，`request_no` 也可作为反查入口。

## 关键列

| 字段 | 类型 | 必填 | 说明 |
|------|------|-----|------|
| `global_id` | bigint | ✅ | 主键，与对应订单的 global_id 完全相同 |
| `issuer_type` | varchar(200) | ✅ | 发起人类型（MERCHANT / PARTNER / USER 等） |
| `issuer_code` | varchar(200) | ✅ | 发起人代码（具体商户 ID） |
| `request_no` | varchar(200) | ✅ | 商户订单号，幂等核心字段 |
| `voucher_type` | varchar(32) |  | 凭证类型（ACQUIRE / REFUND / VOID 等，区分业务类型） |
| `created_time` | timestamp(3) | ✅ | 创建时间 |

## 主键 / 索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `global_id` | 主键 |
| `i_ri_no` | `request_no` | 核心索引：按 request_no 反查订单 |

⚠️ 业务上 `(issuer_type, issuer_code, request_no)` 应当是唯一组合。

## 与关联表的关系

| 关联表 | 关联键 | 关系 | 说明 |
|--------|--------|------|------|
| `t_acquire_order` | `global_id` | 1:1 | 收单订单 |
| `t_refund_order` | `global_id` | 1:1 | 退款订单 |
| `t_void_order` / `t_void_ops_order` | `global_id` | 1:1 | 撤销 / 运营撤销订单 |
| `t_reversal_order` / `t_reversal_orderii` | `global_id` | 1:1 | Reversal 订单 |
| `t_revoke_order` | `global_id` | 1:1 | 冲正订单 |
| `t_deposit_order` | `global_id` | 1:1 | 充值订单 |

所有订单表的 `global_id` 必须能在本表查到对应记录，`voucher_type` 用于区分指向的是哪类订单表。

## 校验点（QA 关注）

1. **幂等核心**：所有订单类业务落库前必须先查 `(issuer_type, issuer_code, request_no)`，命中则直接返回已有订单 `global_id`，不能产生新订单。
2. **request_no 有效性**：商户需保证 request_no 在自身范围内唯一；空值/无效值必须在入口拦截，不能落入本表。
3. **issuer_type + issuer_code 隔离发起人**：防止商户 A 复用商户 B 的 request_no 串单。查询/校验必须三字段联合，**严禁**只用 request_no 单字段判定。
4. **voucher_type 区分业务**：ACQUIRE / REFUND / VOID 等。同一 request_no 在不同 voucher_type 下的处理需符合业务预期（例如退款单的 request_no 与原单 request_no 不应冲突）。
5. **global_id 一致性**：本表 `global_id` 必须与对应订单表（t_acquire_order / t_refund_order / t_void_order …）的 `global_id` 严格相同，1:1 不可漂移。
6. **唯一组合校验**：业务约定 `(issuer_type, issuer_code, request_no)` 唯一。QA 需在并发场景（同请求并发提交）下验证不出现重复登记。
7. **反查链路可用性**：通过 `i_ri_no` 索引按 `request_no` 反查到订单的链路必须可用，是商户查单、对账、客诉排查的基础路径。
8. **MIT/CIT 等多次调用场景**：在 DirectPay 后续 CIT、AutoDebit 代扣等周期性扣款场景下，每次扣款的 request_no 必须唯一登记新记录，不能因签约关系复用历史 request_no。
