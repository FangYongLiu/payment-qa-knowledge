---
id: tbl_fiserv_sale_void_ops_order
object_type: Table
name: Fiserv销售撤销订单表(acquireii.t_fiserv_sale_void_ops_order)
aliases:
- t_fiserv_sale_void_ops_order
- acquireii.t_fiserv_sale_void_ops_order
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-25'
source_type: upload
source_ref: tables/t_fiserv_sale_void_ops_order.md
tags:
- fiserv
- void
- sale-void
related_services: [svc_acquireii]
related_scenarios: []
---

# Fiserv销售撤销订单表(acquireii.t_fiserv_sale_void_ops_order)

## 用途
`acquireii.t_fiserv_sale_void_ops_order` 是 Fiserv 渠道的销售撤销(Sale Void Ops)订单表，记录对原 Fiserv 销售订单的撤销操作(对应通用层 `t_void_order` / `t_void_ops_order`)。

库表:`acquireii.t_fiserv_sale_void_ops_order`。关键区分:
- **Void vs Refund**:Void 仅在原销售所在批次未结算前有效;批次关闭后只能走退款([[tbl_fiserv_refund_order]])。
- **Void vs Reversal**:Reversal([[tbl_fiserv_reversal_order]])多用于通讯异常/超时的协议层冲正;Void 是业务层撤销已成功销售。

## 关联关系
- **所属服务**:[[svc_acquireii]](= frontmatter `related_services`)。
- **关键表**:[[tbl_fiserv_sale_order]](`origin_global_id → global_id` 必须存在的原销售单)、[[tbl_fiserv_batch]](撤销必须在批次关闭前发起)、[[tbl_fiserv_refund_order]] / [[tbl_fiserv_reversal_order]](互斥)、[[tbl_merchant_device]](`device_id` 设备维度溯源)。
- **哪些场景校验它**:POS 刷卡交易落库检查([[scn_pos_transaction_db_check]])。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint ✅ | 主键 |
| `request_no` | varchar(200) ✅ | 请求 No(幂等键) |
| `mis_order_no` | varchar(200) | MIS 订单号 |
| `origin_global_id` | bigint ✅ | 原销售订单号，关联 [[tbl_fiserv_sale_order]] |
| `retransmission` | int ✅ | 重发计数 |
| `type` | varchar(50) | 类型(默认 PURCHASE) |
| `device_id` | varchar(200) ✅ | 设备 ID(关联 [[tbl_merchant_device]]) |
| `partner_id` | varchar(32) ✅ | 商户 ID |
| `res_payload_token` | varchar(32) | 响应负载 Token |
| `channel_param_id` | bigint | 渠道参数 ID |
| `current_cmd_id` | bigint | 当前指令 ID |
| `status` | varchar(50) ✅ | 状态 |
| `fail_code` / `fail_message` / `unity_result_code` | varchar | 错误码/描述/统一结果码 |
| `created_time` / `last_updated_time` | timestamp(3) ✅ | 创建/更新时间 |
| `data_version` | bigint ✅ | 数据版本 |

## 主键 / 索引
- 主键:`global_id`。
- 索引:`i_fsvoo_ogi`(origin_global_id)、`i_fsvoo_rn`(request_no，幂等)、`i_fsvoo_ct`(created_time)、`i_fsvoo_lut`(last_updated_time)。

## 校验点(QA 关注)
- **关联完整性**:`origin_global_id` 必须能在 [[tbl_fiserv_sale_order]] 中找到对应销售订单，且该订单状态为成功。
- **批次时机校验**:撤销创建时间应早于原销售订单所在 [[tbl_fiserv_batch]] 的关闭时间;批次已关闭场景应在 [[tbl_fiserv_refund_order]] 而非本表落库。
- **互斥性**:同一 `origin_global_id` 不应同时存在成功的 Void、Reversal、Refund 记录。
- **重发跟踪**:`retransmission` 计数变化与最终 `status` 是否收敛到终态。
- **幂等键**:同一 `request_no` 重发不应产生重复有效撤销记录。
- **状态与错误码一致性**:失败状态下应有错误码三元组;成功状态下应为空或语义中性。
- **设备/商户一致性**:`device_id`、`partner_id` 应与原销售订单一致。
- **时间序**:`created_time ≤ last_updated_time`，且都晚于原销售订单 `created_time`。
