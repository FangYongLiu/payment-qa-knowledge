---
id: tbl_fiserv_refund_order
object_type: Table
domain: device-pos
status: active
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
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

Fiserv 渠道下的**退款订单**记录表，与通用的 `t_refund_order` 类似但专属 Fiserv 渠道。表名 `acquireii.t_fiserv_refund_order`，重要程度 ⭐⭐⭐⭐。

## 关键列

### 主键和关联
- `global_id` (bigint, 必填)：主键，退款全局号
- `request_no` (varchar(200), 必填)：请求 No
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
- `status` (varchar(50), 必填)：退款状态(如 `FAILED`)
- `fail_code` (varchar(50))：错误码
- `fail_message` (varchar(200))：错误描述
- `unity_result_code` (varchar(200))：统一结果码

### 时间和版本
- `created_time` (timestamp(3), 必填)
- `last_updated_time` (timestamp(3), 必填)
- `data_version` (bigint, 必填)

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | global_id | 主键 |
| `i_frfd_ogi` | origin_global_id | **常用**：通过原订单查退款 |
| `i_frfd_rn` | request_no | 按 request_no 查 |
| `i_frfd_ct` | created_time | 按时间查 |
| `i_frfd_lut` | last_updated_time | 按更新时间查 |

关联表：
- `t_fiserv_sale_order` (N:1)：origin_global_id → global_id
- `t_fiserv_refund_bucket` (N:1)：origin_global_id
- `t_fiserv_channel_param` (1:N)：global_id
- `t_command` (1:1)：current_cmd_id → id

常用查询：
- 通过 `origin_global_id` 查某 Fiserv 销售订单的所有退款，按 `created_time` 排序
- 按 `status = 'FAILED'` + 时间窗口排查失败退款

## 校验点(QA 关注)

1. **退款前必须先查 `t_fiserv_refund_bucket` 检查余额**：校验 refundable_amount 是否充足
2. **本表无 amount 字段**：退款金额不在该表，需到 `channel_param` 或其他关联表查询
3. **`current_cmd_id` 跟踪处理进度**：通过指令系统(`t_command`)执行，关注当前指令的状态推进
4. 失败场景关注 `status` / `fail_code` / `fail_message` / `unity_result_code` 四元组
5. `origin_global_id` 必须能在 `t_fiserv_sale_order` 中找到对应销售订单
6. `request_no` 用于幂等查询，确认外部请求不重复落库
