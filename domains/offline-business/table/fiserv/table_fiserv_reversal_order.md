---
id: tbl_fiserv_reversal_order
object_type: Table
name: Fiserv Reversal订单表(acquireii.t_fiserv_reversal_order)
aliases:
- t_fiserv_reversal_order
- acquireii.t_fiserv_reversal_order
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-25'
source_type: upload
source_ref: tables/t_fiserv_reversal_order.md
tags:
- fiserv
- reversal
- 冲正
related_services: [svc_acquireii]
related_scenarios: []
---

# Fiserv Reversal订单表(acquireii.t_fiserv_reversal_order)

## 用途
Fiserv 渠道的 reversal(反向冲账)订单表。当 Fiserv 接口通信异常(超时、连接断开、未明确响应等)时，需发送 reversal 报文冲销原交易，避免对账方与本地资金状态不一致。本表记录每次 reversal 请求、重发次数及最终状态。重要程度 ⭐⭐⭐(资金风险高):原单可能已在 Fiserv 侧落地、也可能未落地，必须通过 reversal 报文使两侧最终一致。

库表:`acquireii.t_fiserv_reversal_order`。通过 `origin_global_id` 关联原单([[tbl_fiserv_sale_order]] / [[tbl_fiserv_sale_void_ops_order]] / [[tbl_fiserv_refund_order]])。

## 关联关系
- **所属服务**:[[svc_acquireii]](= frontmatter `related_services`,tbl→service 边)。
- **关键表**:[[tbl_fiserv_sale_order]] / [[tbl_fiserv_sale_void_ops_order]] / [[tbl_fiserv_refund_order]](`origin_global_id → global_id` 原单)、[[tbl_fiserv_batch]](结算时需排除 reversal 失败的原单)。
- **哪些场景校验它**:POS 刷卡交易落库检查([[scn_pos_transaction_db_check]])。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint ✅ | 主键 |
| `request_no` | varchar(200) ✅ | 请求 No(幂等键) |
| `mis_order_no` | varchar(200) | mis 订单号 |
| `origin_global_id` | bigint ✅ | 原始订单号(关联原单表 global_id) |
| `type` | varchar(32) ✅ | 冲正类型(区分协议层 / 业务层 reversal) |
| `retransmission` | int ✅ | 重发计数 |
| `device_id` | varchar(200) ✅ | 设备 ID |
| `partner_id` | varchar(32) ✅ | 商户 ID |
| `res_payload_token` | varchar(32) | 响应负载 Token |
| `channel_param_id` | bigint | 渠道参数 ID |
| `current_cmd_id` | bigint | 当前指令 ID |
| `status` | varchar(50) ✅ | 状态(如 `FAILED`、`SUCCESS`) |
| `fail_code` / `fail_message` / `unity_result_code` | varchar | 错误码/描述/统一结果码 |
| `created_time` / `last_updated_time` | timestamp(3) ✅ | 创建/更新时间 |
| `data_version` | bigint ✅ | 数据版本 |

## 主键 / 索引
- 主键:`global_id`。
- 索引:`i_fro_oid`(origin_global_id)、`i_fro_rn`(request_no，幂等)、`i_fro_ct`(created_time)、`i_fro_lut`(last_updated_time)。

## 校验点(QA 关注)
- **失败的 reversal 是资金风险**:`status='FAILED'` 且 `retransmission >= 3` 必须告警、人工跟进。
- **retransmission 重发次数**:监控是否超过阈值(默认 3 次);正常成功的 reversal 重发次数应较小。
- **type 冲正类型**:校验协议层 reversal(通信异常触发)与业务层 reversal(业务校验失败触发)的区分是否正确。
- **origin_global_id 必须能在原单表([[tbl_fiserv_sale_order]] 等)找到对应原单**，否则为孤立 reversal。
- **fail_code / fail_message / unity_result_code** 在失败场景下应非空。
- **request_no 幂等**:同一 request_no 不应重复落库，重发应体现在 `retransmission` 自增而非新增行。
- **原单状态一致性**:reversal 成功后原单状态应被同步冲正。
- **结算排除**:参与 [[tbl_fiserv_batch]] 结算前应排除已被 reversal 成功冲销的原单，避免重复入账。
