---
id: tbl_acquireii_t_refund_order
object_type: Table
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_refund_order.md
tags:
- 退款
- 收单
- DCC
subdomain: acquireii
module: refund
sensitivity: normal
name: 退款订单表
aliases:
- t_refund_order
- acquireii.t_refund_order
related_services:
- svc_acquireii
---

# t_refund_order — 退款订单表

表名：`acquireii.t_refund_order`，重要程度 ⭐⭐⭐⭐⭐。

## 用途

记录收单订单的**退款操作**，每次退款生成一条记录。一笔原订单(`t_acquire_order`)可对应多次退款(部分退款 / 多次退款)。

**典型场景**：
- 商户调用 `refund` 接口 → 写入一条 `t_refund_order`
- 全额退款 / 部分退款 / 多次退款
- DCC 退款时关联 `t_dcc_info` 记录原汇率
- 阿联酋市场带 VAT 税的退款
- 分账订单退款时联动 `t_sharing_info` 决定是否退分账

## 在交易链路中的位置

收单链路上，`t_refund_order` 属于「售后/逆向交易」分支之一，与 `t_void_order`(撤销)、`t_void_ops_order`(运营撤销)、`t_revoke_order`(冲正)、`t_reversal_order` / `t_reversal_orderii`(Reversal) 同级，但语义不同：

- **Refund(退款)**：原订单已结算/已成功，资金从商户回退给消费者，可部分可多次。
- **Void(撤销)**：当日未结算订单的取消，金额必须为全额。
- **Reversal/Revoke**：通讯/系统层面的冲正，处理超时与不一致。

下游链路：退款成功后会驱动 `t_stmt_event` 产生对账事件，并影响 `t_acquire_order` 的可退余额与状态视图。

## 关键列

### 主键和关联
- `global_id` (bigint, ✅) — 主键，退款全局号
- `acquire_global_id` (bigint, ✅) — 原收单订单 global_id，关联 `t_acquire_order`
- `request_no` (varchar(200)) — 请求 No(幂等)，与 `t_request_identity` 配合保证幂等
- `mis_order_no` (varchar(128)) — mis 订单号

### 业务方
- `partner_id` (varchar(200), ✅) — 发起方 memberId
- `device_id` — 设备 ID
- `secondary_merchant_id` (varchar(64)) — 二级商户号
- `operator_name` — 操作员名(谁触发的退款)

### 退款金额
- `currency_code` (varchar(50), ✅) — 退款币种
- `amount` (decimal(19,4), ✅) — 退款金额
- `reason` (varchar(500)) — 退款原因

### 结算和手续费
- `settled_time` — 退款结算时间(资金结算给商户)
- `finished_time` — 完成时间(退款全流程结束)
- `estimated_time` — 预期完成时间
- `settlement_currency` / `settlement_amount` — 结算币种 / 结算金额
- `payee_fee_currency` / `payee_fee_amount` — 退款手续费币种 / 金额

### 含税 / 不含税(阿联酋 VAT)
- `pfbt_crcy` / `pfbt_amt` — 不含税金额币种 / 金额(payee_fee_before_tax)
- `pfv_crcy` / `pf_vat` — VAT 税币种 / VAT 税

### 退款类型
- `refund_usage` — 退款用途
- `refund_type` — 退款类型
- `refund_sharing_amount` — 是否退分账
- `reverted` — 是否退款

### 状态机
- `status` (varchar(200), ✅) — 退款状态
- `fail_code` — 错误码
- `fail_message` — 错误描述
- `unity_result_code` — 统一结果码
- `notify_url` — 商户通知地址

### 其他
- `trade_routing` — 交易路由
- `channel_param_id` — 渠道参数 ID(关联 `t_channel_param`)
- `reserved` — 预留
- `created_time` / `last_updated_time` / `data_version` — 创建/更新/版本

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `global_id` | 主键 |
| `i_ao_ag` | `acquire_global_id` | 常用：通过原订单查所有退款 |
| `i_ao_lut` | `last_updated_time` | 按更新时间扫描 |
| `i_ao_st` | `settled_time` | 按结算时间查 |
| `i_ao_ft` | `finished_time` | 按完成时间查 |

## 关联关系

| 关联表 | 关系 | 说明 |
|--------|------|------|
| `t_acquire_order` | N:1 | `acquire_global_id` → `global_id`，原订单 |
| `t_dcc_info` | 1:1 | DCC 退款时按 `global_id` 关联，记录退款使用的汇率 |
| `t_dcc_info_log` | 1:N | DCC 汇率/金额变更日志 |
| `t_channel_param` | N:1 | `channel_param_id` 关联渠道参数 |
| `t_sharing_info` | 1:N | 分账订单退款时关联分账明细 |
| `t_payment_info` | 通过原订单 | 支付方式信息(原订单) |
| `t_amount_detail` | 1:N | 金额明细拆分 |
| `t_stmt_event` | 1:N | 退款产生的对账事件 |
| `t_request_identity` | 1:1 | `request_no` 幂等校验 |

## 校验点(QA 关注)

1. **退款金额不能超过原订单可退余额**：可退额 = 原订单金额 - 已退款总额(`SUM(t_refund_order.amount) WHERE acquire_global_id = 原订单`)。
2. **DCC 退款必须用原订单汇率**：退款 `t_dcc_info.exchange_rate` 应等于原订单 `t_dcc_info.exchange_rate`，不能用退款时的实时汇率(常见 Bug 点)。
3. **退款手续费独立计算**：`payee_fee_amount` 不一定按比例，需单独验证规则。
4. **时间字段语义区分**：`settled_time`(资金结算给商户) vs `finished_time`(退款全流程结束)，不要混淆。
5. **VAT 税分开记录**：阿联酋市场必须分别校验 `pfbt_amt`(不含税)和 `pf_vat`(税额)，且 `pfbt_amt + pf_vat = payee_fee_amount`。
6. **分账退款**：`refund_sharing_amount` 标识分账订单退款时是否同时退分账，需联动 `t_sharing_info`。
7. **幂等**：通过 `request_no` 校验幂等性，相同 `request_no` 不应产生多条退款记录，防止重复退款。
8. **失败退款监控**：`status = 'FAILED'` 配合 `fail_code` / `fail_message` 排查；可按 `created_time` 近期窗口扫描。
9. **状态一致性**：退款成功后原 `t_acquire_order` 的可退余额视图应同步；全额退款后原订单状态可能流转为 REFUNDED / PARTIAL_REFUNDED。
10. **与 Void 区分**：同一笔订单不应同时存在成功的 Void 和 Refund 记录，QA 用例需覆盖「先 Void 后 Refund 应失败」「已结算后只能 Refund」的边界。

## QA 落库检查要点

- 通过 `acquire_global_id` 反查原 `t_acquire_order`，校验币种、金额、商户三要素一致。
- 部分退款用例：多次写入后 `SUM(amount)` ≤ 原订单金额，最后一次退款若等于剩余额则原单状态变为全额退款。
- DCC 用例：联表 `t_dcc_info` 校验 `exchange_rate`、`settlement_currency`、`settlement_amount` 三者与原订单一致。
- 分账用例：联表 `t_sharing_info` 检查分账退款金额累计与 `refund_sharing_amount` 标识匹配。
- 对账用例：退款成功后应在 `t_stmt_event` 找到对应事件记录。
- 幂等用例：同 `request_no` 重发，DB 中仅有一条 `t_refund_order`。
