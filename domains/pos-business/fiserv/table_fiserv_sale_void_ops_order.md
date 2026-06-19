---
id: tbl_fiserv_sale_void_ops_order
object_type: Table
domain: device-pos
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_fiserv_sale_void_ops_order.md
tags:
- fiserv
- void
- sale-void
subdomain: fiserv
module: void
sensitivity: normal
name: Fiserv销售撤销订单表
aliases:
- t_fiserv_sale_void_ops_order
related_services: []
related_tables:
- tbl_fiserv_batch
- tbl_fiserv_refund_order
- tbl_fiserv_reversal_order
- tbl_fiserv_sale_order
- tbl_merchant_device
related_scenarios:
- scn_fiserv_test_tid_creation
- scn_merchant_transaction_db_check
- scn_pos_transaction_db_check
related_logs: []
related_requirements: []
related_failures: []
---

## 用途与定位

`acquireii.t_fiserv_sale_void_ops_order` 是 Fiserv 渠道的 **销售撤销（Sale Void Ops）订单表**，记录对原 Fiserv 销售订单的撤销操作。对应通用层的 `t_void_order` / `t_void_ops_order`。

### 在交易链路中的位置

```
[POS 刷卡] → t_fiserv_sale_order（原销售单）
                ↓ 撤销请求（批次关闭前）
            t_fiserv_sale_void_ops_order（本表）  ←→ t_fiserv_batch（同批次内）
                ↓ 若批次已关闭则不可 Void，需走
            t_fiserv_refund_order（退款）
                或
            t_fiserv_reversal_order（Reversal 冲正：网络/超时场景）
```

- **Void vs Refund**：Void 仅在原销售所在批次未结算前有效；批次关闭后只能走 Refund。
- **Void vs Reversal**：Reversal 多用于通讯异常/超时的协议层冲正；Void 是业务层撤销已成功销售。

## 关键列

### 主键 / 关联
| 列 | 类型 | 必填 | 说明 |
|----|------|------|------|
| `global_id` | bigint | ✅ | 主键 |
| `request_no` | varchar(200) | ✅ | 请求 No（幂等键） |
| `mis_order_no` | varchar(200) | | MIS 订单号 |
| `origin_global_id` | bigint | ✅ | 原销售订单号，关联 `t_fiserv_sale_order.global_id` |
| `retransmission` | int | ✅ | 重发计数 |
| `type` | varchar(50) | | 类型（默认 PURCHASE） |

### 业务方
| 列 | 类型 | 必填 | 说明 |
|----|------|------|------|
| `device_id` | varchar(200) | ✅ | 设备 ID（关联 `t_merchant_device`） |
| `partner_id` | varchar(32) | ✅ | 商户 ID |

### Fiserv 渠道
| 列 | 类型 | 说明 |
|----|------|------|
| `res_payload_token` | varchar(32) | 响应负载 Token |
| `channel_param_id` | bigint | 渠道参数 ID |
| `current_cmd_id` | bigint | 当前指令 ID |

### 状态机
| 列 | 类型 | 必填 | 说明 |
|----|------|------|------|
| `status` | varchar(50) | ✅ | 状态 |
| `fail_code` | varchar(50) | | 错误码 |
| `fail_message` | varchar(200) | | 错误描述 |
| `unity_result_code` | varchar(200) | | 统一结果码 |

### 时间 / 版本
| 列 | 类型 | 必填 | 说明 |
|----|------|------|------|
| `created_time` | timestamp(3) | ✅ | 创建时间 |
| `last_updated_time` | timestamp(3) | ✅ | 最后更新时间 |
| `data_version` | bigint | ✅ | 数据版本 |

## 主键 / 索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | global_id | 主键 |
| i_fsvoo_ogi | origin_global_id | 通过原销售订单查撤销记录 |
| i_fsvoo_rn | request_no | 按 request_no 查（幂等校验） |
| i_fsvoo_ct | created_time | 按创建时间查 |
| i_fsvoo_lut | last_updated_time | 按更新时间查 |

### 常用查询

```sql
-- 通过原销售订单查撤销记录
SELECT global_id, status, retransmission, fail_code, fail_message, created_time
FROM acquireii.t_fiserv_sale_void_ops_order
WHERE origin_global_id = ?;
```

## 与关联表的关系

| 关联表 | 关联字段 | 关系说明 |
|--------|----------|----------|
| `t_fiserv_sale_order` | `origin_global_id → global_id` | 必须存在的原销售单 |
| `t_fiserv_batch` | 通过原销售订单的批次字段 | 撤销必须在批次未关闭前发起 |
| `t_fiserv_refund_order` | 同 origin 销售单 | 互斥：批次关闭后改走退款，不应再写 Void |
| `t_fiserv_reversal_order` | 同 origin 销售单 | 互斥：通讯异常走 Reversal |
| `t_merchant_device` | `device_id` | 设备维度溯源 |

## QA 落库检查要点

1. **关联完整性**：`origin_global_id` 必须能在 `t_fiserv_sale_order` 中找到对应销售订单，且该订单状态为成功。
2. **批次时机校验**：撤销创建时间应早于原销售订单所在 `t_fiserv_batch` 的关闭时间；批次已关闭场景应在 `t_fiserv_refund_order` 中而非本表落库。
3. **互斥性**：同一 `origin_global_id` 不应同时存在成功的 Void、Reversal、Refund 记录。
4. **重发跟踪 (`retransmission`)**：撤销可能需要多次尝试，关注计数变化与最终 `status` 是否收敛到终态。
5. **幂等键**：同一 `request_no` 的重发不应产生重复有效撤销记录（数量增多但只允许一条最终成功）。
6. **状态与错误码一致性**：失败状态下应有 `fail_code` / `fail_message` / `unity_result_code`；成功状态下这些字段应为空或语义中性。
7. **设备/商户一致性**：`device_id`、`partner_id` 应与原销售订单一致。
8. **时间序**：`created_time ≤ last_updated_time`，且都晚于原销售订单 `created_time`。
9. **data_version**：每次状态变更（含重发）应递增，用于乐观锁校验。
