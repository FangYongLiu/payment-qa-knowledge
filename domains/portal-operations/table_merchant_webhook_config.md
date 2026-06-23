---
id: tbl_merchant_webhook_config
object_type: Table
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_merchant_webhook_config.md
tags:
- webhook
- 商户配置
- 异步通知
subdomain: null
module: null
sensitivity: normal
name: 商户Webhook配置表
aliases:
- t_merchant_webhook_config
- acquireii.t_merchant_webhook_config
related_services:
- svc_merchant
---

## 用途

`t_merchant_webhook_config` 存储**商户级别**的异步通知（webhook）兜底配置。当订单状态发生变化（支付成功 / 退款完成 / 撤销 / 预授权 / 拒付 / 风控拦截）时，收单系统会调用商户配置的 URL 将事件通知到商户侧。

### 与订单级 notify_url 的关系

| 配置位置 | 作用域 | 来源 | 优先级 |
|---|---|---|---|
| `t_acquire_order.notify_url` | 单笔订单 | 创建订单时由商户传入 | 高 |
| `t_merchant_webhook_config.*_notify_url` | 商户全局 | 商户在管理后台/接入流程配置 | 兜底 |

**回调地址解析顺序**：订单级 `notify_url` > 商户级 webhook 配置；订单未指定时才走本表兜底。

## 在交易链路中的位置

本表位于交易**通知/回调环节**，处于交易主流程下游：

1. 收单订单 (`tbl_fiserv_sale_order`) / 退款 (`tbl_fiserv_refund_order`) / 撤销 (`tbl_fiserv_sale_void_ops_order`) / Reversal (`tbl_fiserv_reversal_order`) 等订单状态发生变更；
2. 通知调度器读取订单上的 `notify_url`，若为空则按事件类型 fallback 到本表对应字段（收单→`acquire_notify_url`，退款→`refund_notify_url`，撤销→`void_notify_url`，预授权→`preauth_notify_url`，拒付→`dispute_notify_url`）；
3. 调用失败的通知进入 `t_retryable_command` 进行异步重试。

## 关键列

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `partner_id` | varchar(64) | ✅ | 主键，商户 ID |
| `acquire_notify_url` | varchar(500) |  | 收单通知 URL |
| `refund_notify_url` | varchar(500) |  | 退款通知 URL |
| `void_notify_url` | varchar(500) |  | 撤销通知 URL |
| `preauth_notify_url` | varchar(500) |  | 预授权通知 URL |
| `dispute_notify_url` | varchar(500) |  | 拒付通知 URL |
| `status` | varchar(32) |  | 配置状态 |
| `created_time` | timestamp(3) | ✅ | 创建时间 |
| `last_updated_time` | timestamp(3) | ✅ | 最后更新时间 |

## 主键/索引

- PRIMARY: `partner_id`
- 通过 `partner_id` 关联到商户业务表（如 `t_acquire_order.partner_id`、各 Fiserv 订单表的商户字段）

## 关联表

| 关联表 | 关联键 | 关系说明 |
|---|---|---|
| `tbl_fiserv_sale_order` | `partner_id` | 销售成功后触发收单通知，回调地址走 `acquire_notify_url` 兜底 |
| `tbl_fiserv_refund_order` | `partner_id` | 退款完成触发退款通知，走 `refund_notify_url` 兜底 |
| `tbl_fiserv_sale_void_ops_order` | `partner_id` | 撤销操作触发撤销通知，走 `void_notify_url` 兜底 |
| `tbl_fiserv_reversal_order` | `partner_id` | Reversal 完成时按事件类型路由对应字段 |

## 校验点 (QA 关注)

1. **URL 可访问性**：商户配置后我方系统会主动回调，URL 必须可达，且能在重试窗口内正确响应。
2. **优先级规则**：订单级 `notify_url` 优先于商户级 webhook 配置；订单未指定时才走本表兜底。落库检查时需对照 `t_acquire_order.notify_url` 是否为空。
3. **协议要求**：推荐 HTTPS；HTTP 安全性不足，部分场景/产品会直接拒绝配置。
4. **超时与重试**：通知失败会进入 `t_retryable_command` 重试；需检查重试次数、退避策略与最终失败处理。
5. **签名机制**：webhook 报文通常需要签名（防伪造、防篡改）；商户接入时需校验签名校验逻辑覆盖到所有事件类型。
6. **未配置覆盖**：可通过 `left join t_acquire_order` 排查活跃商户中未配置 webhook 的情况，避免线上交易完成后无法通知商户。
7. **多场景 URL 区分**：收单 / 退款 / 撤销 / 预授权 / 拒付各自独立配置，需分别构造对应类型的事件，验证回调命中正确字段，避免“退款事件打到收单 URL”这类错配。
8. **status 字段**：仅 status 为启用状态的配置才参与回调；停用商户不应再触发通知。
9. **时间字段**：`last_updated_time` 用于排查商户最近一次变更回调地址后是否生效，定位通知地址变更引发的失败问题。
