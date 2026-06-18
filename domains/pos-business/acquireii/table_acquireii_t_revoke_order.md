---
id: tbl_acquireii_t_revoke_order
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_revoke_order.md
tags:
- 冲正
- revoke
- 收单
subdomain: acquireii
module: null
sensitivity: normal
name: 冲正订单表
aliases:
- t_revoke_order
- acquireii.t_revoke_order
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

记录收单订单的**冲正（Revoke）**操作及其状态。冲正是一种**异常订单的纠正操作**，常发生在通信超时、系统异常的场景：

- 商户调用接口超时，不知道订单是否已生效
- 商户发起冲正请求，系统帮助确认订单状态
- 如果原订单成功，则冲正成功后状态恢复正常
- 如果原订单失败/不存在，冲正也算成功（防止"幽灵订单"）

**Revoke vs Void vs Reversal**：
- **Void**：商户主动取消订单
- **Reversal**：系统层面的反向操作（如 ISO 8583 协议层）
- **Revoke**：上层业务的"冲正"语义，处理通信异常

冲正订单本身字段较少，业务参数通过 `t_revoke_order_param` 以 KV 形式扩展关联。

## 关键列

| 字段 | 类型 | 是否必填 | 说明 |
|------|------|---------|------|
| `global_id` | bigint | ✅ | 主键，全局号 |
| `status` | varchar(32) |  | 冲正状态 |
| `fail_code` | varchar(50) |  | 错误码 |
| `fail_message` | varchar(200) |  | 错误描述 |
| `created_time` | timestamp(3) | ✅ | 创建时间 |
| `last_updated_time` | timestamp(3) | ✅ | 最后更新时间 |
| `data_version` | bigint | ✅ | 数据版本 |

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | global_id | 主键 |
| `i_ao_ct` | created_time | 按时间查 |

关联：通过 `global_id` 关联 `t_revoke_order_param`（冲正订单参数，KV 扩展）。

## 校验点(QA 关注)

1. **冲正订单本身字段较少**，业务参数都在 `t_revoke_order_param`，查询时通常需要 LEFT JOIN 取参数。
2. **冲正成功 ≠ 撤销了原订单**，只是确认了原订单的最终状态；如果原订单已成功，冲正后状态恢复正常；如果原订单失败/不存在，冲正也算成功。
3. **冲正失败（status = 'FAILED'）需要人工介入**，可能存在资金风险，需关注 `fail_code` / `fail_message`。
4. 近期失败冲正排查参考：`status = 'FAILED' AND created_time >= DATE_SUB(NOW(), INTERVAL 1 DAY)`。
5. 区分 Revoke / Void / Reversal 三种语义，避免混淆：Revoke 处理的是通信异常下的状态确认，而非主动取消或协议层反向。
