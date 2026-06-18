---
id: tbl_acquireii_t_reversal_order
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_reversal_order.md
tags:
- reversal
- 协议层
- 订单表
subdomain: acquireii
module: reversal
sensitivity: normal
name: Reversal订单表
aliases:
- acquireii.t_reversal_order
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_reversal_order` 用于记录 **reversal**（协议层反向冲账）订单。

- **Reversal**：支付协议层（如 ISO 8583）的反向操作，纠正原订单的资金流向
- 与 **Revoke（冲正，业务层语义）** 区分：reversal 处理"协议层异常时的反向报文"
- 典型场景：交易已下发到卡组织，但应答异常，系统自动发起 reversal 报文，由卡组织根据该报文回滚资金
- 通常由系统自动触发，非商户主动调用
- 新订单走升级版表 `t_reversal_orderii`

## 关键列

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `global_id` | bigint | ✅ | 主键，全局号 |
| `status` | varchar(32) | | reversal 状态（如 `FAILED`） |
| `fail_code` | varchar(50) | | 错误码 |
| `fail_message` | varchar(200) | | 错误描述 |
| `created_time` | timestamp(3) | ✅ | 创建时间 |
| `last_updated_time` | timestamp(3) | ✅ | 最后更新时间 |
| `data_version` | bigint | ✅ | 数据版本 |

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `global_id` | 主键 |
| `i_ao_ct` | `created_time` | 按时间查询 |

通过 `global_id` 可关联主订单与指令系统。

## 校验点（QA 关注）

1. **Reversal 失败有资金风险**：`status = 'FAILED'` 意味着资金已划走但回滚失败，需重点排查
2. 关注 `fail_code` / `fail_message`：定位协议层异常原因
3. 区分 reversal（协议层）与 revoke（业务层冲正），不要混淆语义
4. Reversal 通常由系统自动触发，若出现异常调用来源需告警
5. 新订单已迁移至 `t_reversal_orderii`，本表关注存量数据
6. 常用排查：
   - 近 1 天 reversal：`WHERE created_time >= DATE_SUB(NOW(), INTERVAL 1 DAY)`
   - 失败 reversal：`WHERE status = 'FAILED' ORDER BY created_time DESC`
