---
id: tbl_fiserv_sale_order
object_type: Table
name: Fiserv销售订单表(acquireii.t_fiserv_sale_order)
aliases:
- t_fiserv_sale_order
- acquireii.t_fiserv_sale_order
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-25'
source_type: upload
source_ref: tables/t_fiserv_sale_order.md
tags:
- Fiserv
- 销售订单
- 核心交易表
related_services: [svc_acquireii]
related_scenarios: []
---

# Fiserv销售订单表(acquireii.t_fiserv_sale_order)

## 用途
Fiserv 渠道下的**销售订单**核心交易表，记录通过 Fiserv 渠道发起的 PURCHASE 类交易主单，是 Fiserv 收单交易链路的中心表(与通用 `t_acquire_order` 相对应，但专属 Fiserv 渠道)。重要程度 ⭐⭐⭐⭐⭐。后续退款/撤销/冲正/结算都通过 `global_id` 反查到原销售单。

库表:`acquireii.t_fiserv_sale_order`。链路位置:设备激活 → 开批次 [[tbl_fiserv_batch]](必须先存在) → 销售下单(本表) → 退款 [[tbl_fiserv_refund_order]] / 撤销 [[tbl_fiserv_sale_void_ops_order]] / 冲正 [[tbl_fiserv_reversal_order]] / 结算 [[tbl_pos_settlement]]。

## 关联关系
- **所属服务**:[[svc_acquireii]](= frontmatter `related_services`)。
- **关键表**:[[tbl_fiserv_batch]](交易必须发生在已开启批次内)、[[tbl_fiserv_refund_order]] / [[tbl_fiserv_sale_void_ops_order]] / [[tbl_fiserv_reversal_order]](通过 `global_id → origin_global_id` 回链)、[[tbl_merchant_device]](`device_id + partner_id` 商户-设备绑定)、[[tbl_pos_settlement]](销售单最终归入结算);金额/渠道参数见 [[tbl_acquireii_t_fiserv_channel_param]]。
- **哪些场景校验它**:POS 刷卡交易落库检查([[scn_pos_transaction_db_check]])。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint ✅ | 主键，全局号 |
| `request_no` | varchar(200) ✅ | 请求 No(幂等键) |
| `mis_order_no` | varchar(200) | MIS 订单号 |
| `rcpt_tx_id` | varchar(50) | 收据交易 ID(用户对账用) |
| `type` | varchar(50) | 类型(默认 PURCHASE) |
| `device_id` | varchar(200) ✅ | 设备 ID(对应 [[tbl_hardware_info]] / [[tbl_merchant_device]]) |
| `partner_id` | varchar(32) ✅ | 商户 ID |
| `res_payload_token` | varchar(32) | 响应负载 Token |
| `channel_param_id` | bigint | 渠道参数 ID(关联 [[tbl_acquireii_t_fiserv_channel_param]]) |
| `current_cmd_id` | bigint | 当前指令 ID |
| `status` | varchar(50) ✅ | 订单状态 |
| `fail_code` / `fail_message` / `unity_result_code` | varchar | 失败错误码/描述/统一结果码 |
| `created_time` / `last_updated_time` | timestamp(3) ✅ | 创建/更新时间 |
| `data_version` | bigint ✅ | 数据版本(乐观锁) |

## 主键 / 索引
- 主键:`global_id`。
- 索引:`i_fso_rn`(request_no，幂等)、`i_fso_txid`(rcpt_tx_id，对账)、`i_fso_cci`(current_cmd_id)、`i_fso_ct`(created_time)、`i_fso_lut`(last_updated_time)。

## 校验点(QA 关注)
- **金额不在本表**:在 [[tbl_acquireii_t_payment_info]] 或 channel_param 中，验金额需联查。
- **type 默认 PURCHASE**:可能还有其他类型，断言时注意区分。
- **rcpt_tx_id**:收据上的交易号，应非空且唯一。
- **必须先有批次**:设备必须先在 [[tbl_fiserv_batch]] 开批次才能交易，否则销售单不应落库或应为失败态。
- **status 终态**:成功应为 `SUCCESS`;失败时 `fail_code` / `fail_message` / `unity_result_code` 应有值。
- **request_no 幂等**:相同 request_no 重复请求应返回同一 global_id。
- **channel_param_id 必填**:Fiserv 交易必须绑定有效渠道参数。
- 常用查询:`device_id` + `DATE(created_time)` 查某天交易;`status='SUCCESS'` 近 7 天成功率;`global_id` 反查退款/撤销/冲正。
