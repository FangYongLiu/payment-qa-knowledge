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
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_request_identity` 是收单系统**幂等防重的核心表**，登记每个商户请求的 `request_no`，保证同一商户的相同请求不会产生两笔订单。

**典型场景**：
- 商户调用 placeOrder 接口，传入 request_no = "ABC123"
- 系统先在 t_request_identity 查找
- 已存在 → 直接返回已有订单（幂等）
- 不存在 → 创建新订单并登记到本表

所有订单类业务（t_acquire_order / t_refund_order 等）都通过 `global_id` 或 `request_no` 与本表 1:1 关联。

## 关键列

| 字段 | 类型 | 必填 | 说明 |
|------|------|-----|------|
| `global_id` | bigint | ✅ | 主键，与对应订单的 global_id 相同 |
| `issuer_type` | varchar(200) | ✅ | 发起人类型（MERCHANT / PARTNER / USER 等） |
| `issuer_code` | varchar(200) | ✅ | 发起人代码（具体商户 ID） |
| `request_no` | varchar(200) | ✅ | 商户订单号，核心字段 |
| `voucher_type` | varchar(32) |  | 凭证类型（可能是 ACQUIRE / REFUND / VOID 等） |
| `created_time` | timestamp(3) | ✅ | 创建时间 |

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `global_id` | 主键 |
| `i_ri_no` | `request_no` | 核心索引：按 request_no 查询 |

⚠️ 业务上 `(issuer_type, issuer_code, request_no)` 应当是唯一组合。

## 校验点(QA 关注)

1. **幂等核心**：所有订单类业务都依赖此表防重，落库前必须先查 `(issuer_type, issuer_code, request_no)`，命中则返回已有订单 global_id。
2. **request_no 必须有效**：商户需保证 request_no 在自身范围内唯一；空值/无效值需在入口拦截。
3. **issuer_type + issuer_code 隔离发起人**：防止商户 A 复用商户 B 的 request_no 串单，查询/校验必须三字段联合，不能只用 request_no。
4. **voucher_type 区分业务**：ACQUIRE / REFUND / VOID 等，校验同一 request_no 在不同 voucher_type 下的处理是否符合预期。
5. **global_id 一致性**：本表 global_id 必须与对应订单表（t_acquire_order / t_refund_order 等）的 global_id 严格相同，1:1 关联。
6. **唯一组合校验**：业务约定 `(issuer_type, issuer_code, request_no)` 唯一，QA 需验证并发场景下是否存在重复登记。
7. **反查链路**：通过 `i_ri_no` 索引按 request_no 反查订单的链路必须可用。
