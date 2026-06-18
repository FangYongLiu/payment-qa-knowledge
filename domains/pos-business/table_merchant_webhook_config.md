---
id: tbl_merchant_webhook_config
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
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
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储商户级别的异步通知（webhook）兜底配置。当订单状态变化（支付成功/退款完成/撤销/预授权/拒付/风控拦截）时，系统调用商户配置的 URL 通知商户。

**与 `t_acquire_order.notify_url` 的区别**：
- `t_acquire_order.notify_url`：订单级别的回调地址（创建订单时传入）
- `t_merchant_webhook_config`：商户级别的兜底配置（订单未指定时使用）

**优先级**：订单级 notify_url > 商户级配置。

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
- 通过 `partner_id` 关联到商户业务表

## 校验点(QA 关注)
1. **URL 可访问性**：商户配置后我方系统会回调，URL 必须可达
2. **优先级规则**：订单级 `notify_url` 优先于商户级 webhook 配置；订单未指定时才走该表兜底
3. **协议要求**：推荐 HTTPS，HTTP 不够安全，部分场景会拒绝
4. **超时与重试**：通知失败会进入 `t_retryable_command` 重试
5. **签名机制**：webhook 内容通常需要签名以防伪造
6. **未配置覆盖**：可通过 left join `t_acquire_order` 排查活跃商户中未配置 webhook 的情况
7. **多场景 URL 区分**：收单/退款/撤销/预授权/拒付各自独立配置，需分别校验对应场景的回调走向正确字段
