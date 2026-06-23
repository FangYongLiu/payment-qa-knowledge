---
id: tbl_fiserv_refund_order
object_type: Table
domain: device-pos
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_fiserv_refund_order.md
tags:
- fiserv
- refund
- order
subdomain: fiserv
module: refund
sensitivity: normal
name: Fiserv退款订单表
aliases:
- t_fiserv_refund_order
- acquireii.t_fiserv_refund_order
related_services: []
related_tables:
- tbl_fiserv_batch
- tbl_fiserv_reversal_order
- tbl_fiserv_sale_order
- tbl_fiserv_sale_void_ops_order
- tbl_pos_settlement
- tbl_pos_settlement_history
related_scenarios:
- scn_fiserv_test_tid_creation
- scn_merchant_transaction_db_check
- scn_pos_transaction_db_check
related_logs: []
related_requirements: []
related_failures: []
---

## 用途与定位

`acquireii.t_fiserv_refund_order` 是 **Fiserv 渠道专属的退款订单表**，记录通过 Fiserv 收单通道发起的退款交易。重要程度 ⭐⭐⭐⭐。

该表与通用 `t_refund_order` 角色类似，但只服务 Fiserv 渠道；与 `t_fiserv_sale_order`（销售）、`t_fiserv_sale_void_ops_order`（销售撤销）、`t_fiserv_reversal_order`（Reversal）共同构成 Fiserv 渠道的交易订单族。

## 在交易链路中的位置

```
持卡人/POS → t_fiserv_sale_order(销售)
                  │
                  ├── 当日撤销 → t_fiserv_sale_void_ops_order
                  ├── 通讯异常 → t_fiserv_reversal_order
                  └── 已结算后退款 → t_fiserv_refund_order  ← 本表
                                          │
                                          ├── 余额校验 → t_fiserv_refund_bucket
                                          ├── 渠道参数 → t_fiserv_channel_param
                                          ├── 指令执行 → t_command
                                          └── 入批/结算 → t_fiserv_batch / t_pos_settlement
```

退款发起后，通过 `current_cmd_id` 关联到 `t_command` 推进状态机；成功后会进入 Fiserv 批次（`t_fiserv_batch`）并最终影响 POS 结算（`t_pos_settlement` / `t_pos_settlement_history`）。

## 关键列

### 主键和关联
- `global_id` (bigint, 必填)：主键，退款全局号
- `request_no` (varchar(200), 必填)：请求 No，用于幂等
- `mis_order_no` (varchar(200))：mis 订单号
- `origin_global_id` (bigint, 必填)：**原销售订单 global_id**，关联 `t_fiserv_sale_order.global_id`

### 业务方
- `device_id` (varchar(200), 必填)：设备 ID
- `partner_id` (varchar(32), 必填)：商户 ID

### Fiserv 渠道相关
- `res_payload_token` (varchar(32))：响应负载 Token
- `channel_param_id` (bigint)：渠道参数 ID
- `current_cmd_id` (bigint)：当前指令 ID，关联 `t_command.id`

### 状态机
- `status` (varchar(50), 必填)：退款状态（如 `FAILED`）
- `fail_code` (varchar(50))：错误码
- `fail_message` (varchar(200))：错误描述
- `unity_result_code` (varchar(200))：统一结果码

### 时间和版本
- `created_time` (timestamp(3), 必填)
- `last_updated_time` (timestamp(3), 必填)
- `data_version` (bigint, 必填)

## 主键 / 索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | global_id | 主键 |
| `i_frfd_ogi` | origin_global_id | **最常用**：通过原销售订单查所有退款 |
| `i_frfd_rn` | request_no | 按 request_no 幂等查询 |
| `i_frfd_ct` | created_time | 按创建时间查 |
| `i_frfd_lut` | last_updated_time | 按更新时间查 |

## 关联表

| 关联表 | 关系 | 关联键 | 说明 |
|--------|------|--------|------|
| `t_fiserv_sale_order` | N:1 | `origin_global_id → global_id` | 原销售订单 |
| `t_fiserv_refund_bucket` | N:1 | `origin_global_id` | 退款额度桶（余额校验） |
| `t_fiserv_channel_param` | 1:N | `global_id` | Fiserv 渠道参数（含金额、卡信息等） |
| `t_command` | 1:1 | `current_cmd_id → id` | 当前处理指令，跟踪状态推进 |
| `t_fiserv_batch` | — | 通过批次流程 | 退款成功后入批 |

## 常用查询

- 通过 `origin_global_id` 查某 Fiserv 销售订单的全部退款，按 `created_time` 排序
- `status = 'FAILED'` + 时间窗口排查失败退款
- 按 `request_no` 幂等查询，确认外部请求不重复落库

## QA 落库检查要点

1. **本表无 amount 字段**：退款金额需到 `t_fiserv_channel_param` 或其他关联表查询，**不要在本表找金额**。
2. **退款前必须先查 `t_fiserv_refund_bucket`**：校验 `refundable_amount` 是否充足，避免超额退款。
3. **`origin_global_id` 必须能在 `t_fiserv_sale_order` 中找到**对应销售订单，否则属于脏数据。
4. **指令进度跟踪**：通过 `current_cmd_id → t_command` 查看当前指令状态，确认是否在推进中或已终态。
5. **失败场景四元组**：联合关注 `status` / `fail_code` / `fail_message` / `unity_result_code`，定位失败根因。
6. **幂等校验**：同一 `request_no` 不应产生多条退款记录。
7. **状态一致性**：退款成功后，`t_fiserv_refund_bucket` 的可退余额应相应扣减，`t_fiserv_batch` 中应能找到对应批次记录。
8. **结算影响**：成功退款最终会反映在 `t_pos_settlement` / `t_pos_settlement_history`，对账时需联动校验。
