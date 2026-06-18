---
id: tbl_fiserv_sale_void_ops_order
object_type: Table
domain: pos-business
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
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

Fiserv 渠道的 **销售撤销（sale void ops）** 订单表，记录对原 Fiserv 销售订单的撤销操作。表名 `acquireii.t_fiserv_sale_void_ops_order`，对应通用的 `t_void_order`、`t_void_ops_order`。通过 `origin_global_id` 关联到原销售订单（`t_fiserv_sale_order`），支持重发跟踪。

## 关键列

### 主键 / 关联
- `global_id` bigint ✅ 主键
- `request_no` varchar(200) ✅ 请求 No
- `mis_order_no` varchar(200) mis 订单号
- `origin_global_id` bigint ✅ 原销售订单号（关联 `t_fiserv_sale_order.global_id`）
- `retransmission` int ✅ 重发计数
- `type` varchar(50) 类型（默认 PURCHASE）

### 业务方
- `device_id` varchar(200) ✅ 设备 ID
- `partner_id` varchar(32) ✅ 商户 ID

### Fiserv 渠道
- `res_payload_token` varchar(32) 响应负载 Token
- `channel_param_id` bigint 渠道参数 ID
- `current_cmd_id` bigint 当前指令 ID

### 状态机
- `status` varchar(50) ✅ 状态
- `fail_code` varchar(50) 错误码
- `fail_message` varchar(200) 错误描述
- `unity_result_code` varchar(200) 统一结果码

### 时间 / 版本
- `created_time` timestamp(3) ✅ 创建时间
- `last_updated_time` timestamp(3) ✅ 最后更新时间
- `data_version` bigint ✅ 数据版本

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | global_id | 主键 |
| i_fsvoo_ogi | origin_global_id | 通过原订单查 |
| i_fsvoo_rn | request_no | 按 request_no 查 |
| i_fsvoo_ct | created_time | 按时间查 |
| i_fsvoo_lut | last_updated_time | 按更新时间查 |

常用查询：通过 `origin_global_id` 查询某销售订单对应的撤销记录（status、retransmission、fail_message、created_time）。

## 校验点(QA 关注)

1. **retransmission 跟踪重发**：撤销可能需要多次尝试，关注该值变化与最终 status。
2. **撤销时机**：撤销必须在批次结束前完成；批次关闭后只能走退款流程，不应再产生 void ops 记录。
3. **关联完整性**：`origin_global_id` 必须能在 `t_fiserv_sale_order` 中找到对应销售订单。
4. **状态与错误码一致性**：失败状态下应有 `fail_code` / `fail_message` / `unity_result_code`。
5. **重发幂等**：同一 `request_no` 的重发应不产生重复有效撤销。
