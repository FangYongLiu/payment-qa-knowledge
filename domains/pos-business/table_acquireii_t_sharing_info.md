---
id: tbl_acquireii_t_sharing_info
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_sharing_info.md
tags:
- 分账
- split-payment
subdomain: null
module: null
sensitivity: normal
name: 分账信息表
aliases:
- t_sharing_info
- acquireii.t_sharing_info
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_amount_detail
- tbl_acquireii_t_payment_info
- tbl_acquireii_t_refund_order
- tbl_acquireii_t_secondary_merchant_detail
related_scenarios:
- scn_acquire_product_apply
- scn_merchant_transaction_db_check
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_sharing_info`（分账信息表）记录一笔订单的**分账信息**。一笔交易可能拆分给多个收款方，每个分账方对应一条记录。

典型场景：平台型商户（外卖、电商）一笔订单拆分给平台、店家、配送员等多方，一笔订单对应多条 `t_sharing_info` 记录。

重要程度：⭐⭐⭐⭐

## 在交易链路中的位置

```
t_acquire_order (订单主表)
      │ global_id = payment_global_id
      ├──> t_payment_info        (支付通道信息)
      ├──> t_amount_detail       (金额明细)
      ├──> t_sharing_info  ←★ 本表（N 条，按收款方拆分）
      │           │ sharing_mid
      │           └──> t_secondary_merchant_detail (二级商户)
      └──> t_refund_order        (退款时根据 refund_sharing_amount 决定是否回退分账)
```

本表位于**订单成功后**的资金分配环节，是平台型业务（marketplace / 外卖 / 电商）的核心账务依据。

## 关键列

### 主键与关联
- `id` bigint：主键
- `sharing_no` varchar(64)：分账流水号（分账维度，与订单号不同）
- `sharing_identity` varchar(64)：分账标识（可能是平台 ID、活动 ID 等，含义不固定）
- `payment_global_id` bigint：关联订单 global_id（关联 `t_acquire_order` / `t_refund_order`）

### 分账参与方
- `sharing_mid` varchar(50)：分账方 MID（收款方账户，关联二级商户）
- `inst_code` varchar(32)：机构代码

### 分账金额
- `sharing_amount` decimal(18,4)：分账金额
- `sharing_amount_cur` varchar(50)：分账金额币种（可能与订单币种不同）
- `currency_code` varchar(50)：币种

### 分账类型
- `sharing_type` varchar(32)：分账类型
- `sharing_reason` varchar(255)：分账原因

### 状态与回执
- `status` varchar(32)：分账状态（如 SUCCESS / FAILED）
- `fail_code` varchar(50)：错误码
- `fail_msg` varchar(200)：错误描述

### 时间与版本
- `request_time` timestamp(3)：请求时间
- `finish_time` timestamp(3)：完成时间
- `created_time` timestamp(3)：创建时间
- `last_updated_time` timestamp(3)：最后更新时间
- `data_version` bigint：数据版本

## 主键 / 索引
- PRIMARY：`id`
- `i_si_pgi`：`payment_global_id`（**最常用**，按订单查分账）
- `i_si_sn`：`sharing_no`
- `i_si_smid`：`sharing_mid`
- `i_si_ct`：`created_time`

## 关联表

| 关联表 | 关系 | 关联键 | 说明 |
|---|---|---|---|
| `t_acquire_order` | N:1 | `payment_global_id → global_id` | 一笔订单可拆为多条分账 |
| `t_refund_order` | N:1 | `payment_global_id → global_id` | 退款时按 `refund_sharing_amount` 判断是否回退分账 |
| `t_secondary_merchant_detail` | N:1 | `sharing_mid → mid` | 分账收款方即二级商户 |
| `t_amount_detail` | 同订单 | `payment_global_id` | 订单金额拆分明细，与分账金额需对账一致 |
| `t_payment_info` | 同订单 | `payment_global_id` | 主交易通道信息 |

## QA 落库检查要点

1. **分账总额验证**：部分场景下 `sum(sharing_amount) == 订单 total_amount`，但也可能有手续费独立扣除，验证时需结合业务规则与 `t_amount_detail`。
2. **退款是否退分账**：由 `t_refund_order.refund_sharing_amount` 决定——Y 表示退款同时回退分账；N 表示只退商户款、分账不退（已支付给二级商户）。
3. **sharing_no 与订单号不同**：`sharing_no` 是分账维度的流水号，不要与 `payment_id` / `merchant_order_no` 混用。
4. **多币种处理**：`sharing_amount_cur` 可能与订单币种不一致，对账时注意按币种维度聚合。
5. **sharing_identity 含义不固定**：可能是平台 ID、活动 ID 等业务标识，需结合上下文解读。
6. **状态扫描走索引**：`status` 字段无索引，按状态查询应配合 `created_time`（`i_si_ct`）使用，避免全表扫描。
7. **失败分账监控**：关注 `status='FAILED'` 的记录及 `fail_code` / `fail_msg`，定位渠道侧或账户侧失败原因。
8. **必填字段非空校验**：`id`、`sharing_no`、`payment_global_id`、`sharing_mid`、`created_time`、`last_updated_time`、`data_version` 不可为空。
9. **按订单查分账**：使用 `payment_global_id`（走 `i_si_pgi`），核对每个 `sharing_mid` 对应一条记录且 `status=SUCCESS`。
10. **二级商户一致性**：`sharing_mid` 应能在 `t_secondary_merchant_detail` 中查到对应商户配置。
