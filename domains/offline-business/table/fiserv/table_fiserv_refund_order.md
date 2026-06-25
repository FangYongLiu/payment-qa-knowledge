---
id: tbl_fiserv_refund_order
object_type: Table
name: Fiserv退款订单表(acquireii.t_fiserv_refund_order)
aliases:
- t_fiserv_refund_order
- acquireii.t_fiserv_refund_order
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-25'
source_type: upload
source_ref: tables/t_fiserv_refund_order.md
tags:
- fiserv
- refund
- order
related_services: [svc_acquireii]
related_scenarios: []
---

# Fiserv退款订单表(acquireii.t_fiserv_refund_order)

## 用途
`acquireii.t_fiserv_refund_order` 是 Fiserv 渠道专属的退款订单表，记录通过 Fiserv 收单通道发起的退款交易。重要程度 ⭐⭐⭐⭐。与 [[tbl_fiserv_sale_order]](销售)、[[tbl_fiserv_sale_void_ops_order]](撤销)、[[tbl_fiserv_reversal_order]](冲正)共同构成 Fiserv 渠道交易订单族。退款用于「已结算后退款」场景(批次关闭后 Void 不再有效，只能走退款)。

库表:`acquireii.t_fiserv_refund_order`。退款发起后通过 `current_cmd_id` 关联指令推进状态机;成功后进入 Fiserv 批次([[tbl_fiserv_batch]])并最终影响 POS 结算([[tbl_pos_settlement]] / [[tbl_pos_settlement_history]])。

## 关联关系
- **所属服务**:[[svc_acquireii]](= frontmatter `related_services`,tbl→service 边)。
- **关键表**:[[tbl_fiserv_sale_order]](`origin_global_id → global_id` 原销售单)、`t_fiserv_refund_bucket`(退款额度桶/余额校验，对象待补)、[[tbl_acquireii_t_fiserv_channel_param]](渠道参数含金额)、[[tbl_fiserv_batch]] / [[tbl_pos_settlement]] / [[tbl_pos_settlement_history]](入批/结算)。
- **哪些场景校验它**:POS 刷卡交易落库检查([[scn_pos_transaction_db_check]])。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint ✅ | 主键，退款全局号 |
| `request_no` | varchar(200) ✅ | 请求 No(幂等) |
| `mis_order_no` | varchar(200) | mis 订单号 |
| `origin_global_id` | bigint ✅ | 原销售订单 global_id，关联 [[tbl_fiserv_sale_order]] |
| `device_id` | varchar(200) ✅ | 设备 ID |
| `partner_id` | varchar(32) ✅ | 商户 ID |
| `res_payload_token` | varchar(32) | 响应负载 Token |
| `channel_param_id` | bigint | 渠道参数 ID |
| `current_cmd_id` | bigint | 当前指令 ID(关联 t_command) |
| `status` | varchar(50) ✅ | 退款状态(如 `FAILED`) |
| `fail_code` / `fail_message` / `unity_result_code` | varchar | 错误码/描述/统一结果码 |
| `created_time` / `last_updated_time` | timestamp(3) ✅ | 创建/更新时间 |
| `data_version` | bigint ✅ | 数据版本 |

> 本表无 amount 字段，退款金额需到 [[tbl_acquireii_t_fiserv_channel_param]] 或其他关联表查询。

## 主键 / 索引
- 主键:`global_id`。
- 索引:`i_frfd_ogi`(origin_global_id，最常用，按原销售单查退款)、`i_frfd_rn`(request_no)、`i_frfd_ct`(created_time)、`i_frfd_lut`(last_updated_time)。

## 校验点(QA 关注)
- **本表无金额字段**:不要在本表找金额。
- **退款前必须先查 `t_fiserv_refund_bucket`**:校验 `refundable_amount` 是否充足，避免超额退款。
- **`origin_global_id` 必须能在 [[tbl_fiserv_sale_order]] 中找到**对应销售订单，否则属脏数据。
- **指令进度**:通过 `current_cmd_id → t_command` 查看当前指令状态。
- **失败四元组**:联合关注 `status` / `fail_code` / `fail_message` / `unity_result_code` 定位根因。
- **幂等**:同一 `request_no` 不应产生多条退款记录。
- **状态一致性**:退款成功后退款桶可退余额应相应扣减，[[tbl_fiserv_batch]] 中应能找到对应批次。
- **结算影响**:成功退款最终反映在 [[tbl_pos_settlement]] / [[tbl_pos_settlement_history]]，对账时联动校验。
