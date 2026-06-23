---
id: tbl_acquireii_t_preauth_control
object_type: Table
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_preauth_control.md
tags:
- preauth
- capture
- authorization
subdomain: preauth
module: null
sensitivity: normal
name: 预授权控制表
aliases:
- t_preauth_control
- acquireii.t_preauth_control
related_services:
- svc_acquireii
---

## 用途

`acquireii.t_preauth_control` 记录**预授权订单**的资金占用与 Capture 进度，是预授权业务的核心控制表，管理授权金额、Capture 进展、过期与撤销状态。重要程度 ⭐⭐⭐⭐。

**预授权（Pre-Authorization）业务模式**：
- 商户先冻结一笔资金（authorize），实际消费确认后再扣款（capture）
- 实际金额可能小于授权金额，需要部分释放
- 典型场景：酒店入住冻结 1000、退房实扣 800；加油站先冻结 500、按实际加油量扣款

## 在交易链路中的位置

```
t_acquire_order (订单主表)
    │ 1:1  global_id
    ├─→ t_preauth_control (本表，预授权汇总/控制)
    │       │ 1:N  global_id → preauth_order_id
    │       └─→ t_preauth_relation (每次 capture 明细)
    ├─→ t_payment_info (支付信息)
    ├─→ t_amount_detail (金额明细)
    └─→ t_void_order (撤销订单，对应 void_flag=Y)
```

本表为预授权的**汇总/控制视图**，`t_preauth_relation` 为每次 capture 的明细记录。

## 关键列

**主键与授权总金额**：
- `global_id` (bigint，主键)：对应订单 global_id
- `amount` (decimal(19,4))：授权总金额（最大值）
- `amount_currency` (char(3))：授权金额币种

**Capture 进度（金额三态）**：
- `captured_amount` (decimal(19,4))：已 capture 金额（已实际扣款）
- `captured_amt_cur` (char(3))：已 capture 币种
- `capturing_amount` (decimal(19,4))：capturing 中金额（处理中）
- `capturing_amt_cur` (char(3))：capturing 币种
- 可用余额 = amount - captured_amount - capturing_amount

**业务标识**：
- `partner_id` (varchar(64))：商户 ID
- `expire_date` (timestamp(3))：预授权过期时间
- `authorization_id` (varchar(64))：授权 ID（外部系统标识）
- `inst_code` (varchar(32))：机构代码
- `void_flag` (varchar(3))：是否已撤销（Y/N）

**时间与版本**：
- `created_time`、`last_updated_time` (timestamp(3))
- `data_version` (bigint)

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | global_id | 主键 |
| `i_pc_ct` | created_time | 按时间查询 |
| `i_pc_aid` | authorization_id | 按授权 ID 查询 |

## 关联表

| 关联表 | 关系 | 关联字段 | 说明 |
|--------|------|----------|------|
| `t_acquire_order` | 1:1 | global_id | 订单主表，预授权订单的基础信息 |
| `t_preauth_relation` | 1:N | global_id → preauth_order_id | 每次 capture 的明细，本表为汇总 |
| `t_payment_info` | 1:1 | global_id | 支付通道与卡信息 |
| `t_amount_detail` | 1:N | global_id | 金额组成明细 |
| `t_void_order` | 关联 | global_id | 当 `void_flag='Y'` 时对应撤销订单 |

## 校验点（QA 关注）

1. **Capture 不能超额**：业务约束 `captured_amount + capturing_amount ≤ amount`，超额属于异常数据。
2. **过期后不能 capture**：超过 `expire_date` 后授权失效，需校验过期前完成 capture。
3. **撤销后不能 capture**：`void_flag='Y'` 表示已撤销，撤销后不允许再 capture，应同步存在 `t_void_order` 记录。
4. **金额三态币种一致性**：`amount_currency` / `captured_amt_cur` / `capturing_amt_cur` 应保持一致。
5. **多次 capture 累加正确**：一笔预授权可分多次扣款，需验证 `captured_amount` 累加正确，且与 `t_preauth_relation` 全部明细汇总一致。
6. **即将过期监控**：`expire_date` 在 24 小时内、`void_flag != 'Y'` 且 `captured_amount < amount` 的记录需关注是否会失效。
7. **可用余额计算**：`available_amount = amount - captured_amount - capturing_amount`，不应为负。
8. **主表一致性**：`global_id` 必须能在 `t_acquire_order` 中找到对应订单，且订单类型应为预授权。

## QA 落库检查要点

- 创建预授权订单后：本表应生成一条记录，`amount` = 授权金额，`captured_amount=0`，`capturing_amount=0`，`void_flag='N'`，`expire_date` 已设置。
- 发起 capture 中：`capturing_amount` 增加；capture 成功后 `capturing_amount` 减少、`captured_amount` 增加，且 `t_preauth_relation` 新增明细。
- 撤销预授权：`void_flag` 由 N → Y，且 `t_void_order` 存在对应记录。
- 部分 capture 后剩余金额释放：剩余金额 = amount - captured_amount，需确认资金释放逻辑触发。
- 跨表对账：本表 `captured_amount` = SUM(`t_preauth_relation` 中所有 capture 成功明细金额)。
