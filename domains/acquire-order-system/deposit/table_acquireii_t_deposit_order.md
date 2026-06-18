---
id: tbl_acquireii_t_deposit_order
object_type: Table
domain: acquire-order-system
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_deposit_order.md
tags:
- deposit
- 充值
- kiosk
- wallet
subdomain: deposit
module: null
sensitivity: normal
name: 充值订单表
aliases:
- t_deposit_order
- acquireii.t_deposit_order
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_amount_detail
- tbl_acquireii_t_card_info
- tbl_acquireii_t_command
- tbl_acquireii_t_payment_info
- tbl_acquireii_t_refund_order
- tbl_acquireii_t_request_identity
- tbl_acquireii_t_reversal_order
related_scenarios:
- scn_merchant_transaction_db_check
- scn_payby_withdraw_core_cases
related_logs: []
related_requirements: []
related_failures: []
---

## 表用途

`acquireii.t_deposit_order`（充值订单表）记录用户向钱包/账户**充值（deposit）**的订单数据。与 `t_acquire_order`（商户收单 B2C 支付）业务结构相似，但**面向 C2 钱包入金**场景。

主键 `global_id`，重要程度 ⭐⭐⭐⭐。

典型场景：
- 用户在 Kiosk（自助终端）扫码充值
- 用户向自己的 Wallet 入金
- 用户向特定 QR 码（如商家收款码）充值

## 在交易链路中的位置

充值（Deposit）作为 acquireII 体系下与收单并列的一条入金链路：

```
请求侧 (request_no/voucher_no)
   │
   ▼
t_request_identity （请求标识、幂等）
   │
   ▼
t_deposit_order  ← 本表（充值订单主单）
   │   ├── 通过 global_id 关联
   │   ▼
t_payment_info   （支付完成信息：渠道、清算、流水）
t_card_info      （卡支付信息，若走卡通道）
t_command        （指令调度，渠道交互）
   │
   ▼
（如发生退款/冲正）t_refund_order / t_reversal_order
```

与 `t_acquire_order` 的差异：
- `t_acquire_order`：商户收单（B2C 支付，消费者付给商户）
- `t_deposit_order`：用户充值（C2 钱包入金，资金进入钱包/账户）

两表结构相似，下游表（payment_info / card_info / command）通过 `global_id` 共用。

## 关键字段

### 主键和标识
| 字段 | 类型 | 说明 |
|------|------|------|
| `global_id` | bigint | 主键，全局号，下游表关联键 |
| `request_no` | varchar(200) | 等同于 requestIdentity.requestNo |
| `voucher_no` | varchar(200) | 凭证号 |

### 业务方信息
| 字段 | 类型 | 说明 |
|------|------|------|
| `member_partner_id` | varchar(200) | memberPartnerId |
| `partner_id` | varchar(200) | 发起方 memberId |
| `member_id` | varchar(200) | **收款人 mid（充值目标钱包/账户）** |
| `product_code` | varchar(200) | 产品码 |

### 充值金额
| 字段 | 类型 | 说明 |
|------|------|------|
| `currency_code` | varchar(50) | 充值币种 |
| `amount` | decimal(19,4) | 充值金额 |
| `qr_code` | varchar(200) | 二维码（**唯一约束**） |

### 业务信息
| 字段 | 类型 | 说明 |
|------|------|------|
| `subject` | varchar(200) | 标题 |
| `notify_url` | varchar(500) | 通知地址 |
| `request_time` | timestamp(3) | 请求时间 |
| `inst_code` | varchar(32) | 机构代码 |
| `kiosk_id` | varchar(100) | Kiosk 设备 ID（非 Kiosk 充值为 NULL） |

### 状态机
| 字段 | 类型 | 说明 |
|------|------|------|
| `status` | varchar(200) | 充值订单状态 |
| `fail_code` | varchar(50) | 错误码 |
| `fail_message` | varchar(200) | 错误描述 |
| `unity_result_code` | varchar(200) | 统一结果码 |

### 时间和版本
| 字段 | 类型 | 说明 |
|------|------|------|
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本（乐观锁） |

## 主键 / 索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `global_id` | 主键 |
| `ui_t_d_o_qr_code` | `qr_code` | 唯一约束（一个 QR 码对应一笔订单） |
| `i_ao_ct` | `created_time` | 按创建时间查 |
| `i_ao_lut` | `last_updated_time` | 按更新时间扫批 |

## 与关联表的关系

- **`t_request_identity`**：通过 `request_no` 对齐，校验幂等。
- **`t_payment_info`**：通过 `global_id` 关联，记录充值最终支付信息（渠道流水、清算等）。
- **`t_card_info`**：通过 `global_id` 关联，若充值走卡通道则记录卡信息。
- **`t_command` / 可重试/不可重试指令表**：通过 `global_id` 关联，记录调度渠道的指令执行轨迹。
- **`t_amount_detail`**：若有费用/分项金额拆解，可通过 `global_id` 关联。
- **`t_refund_order` / `t_reversal_order`**：充值若需退回或冲正，通过原 `global_id` 反查。
- **`t_acquire_order`**：**并列但不同业务**——查询统计时务必区分。

## QA 落库检查要点

1. **qr_code 唯一约束**：同一个 QR 码不能创建两笔订单，重复创建应被唯一索引 `ui_t_d_o_qr_code` 拦截，返回唯一键冲突。
2. **kiosk_id 区分场景**：
   - Kiosk 充值场景：`kiosk_id` 必填
   - 非 Kiosk 充值：`kiosk_id` 为 NULL
   - 做 Kiosk 维度统计时需按 `kiosk_id IS NOT NULL` 过滤。
3. **member_id / partner_id 语义不要弄反**：
   - `member_id` = **收款人**（充值目标钱包/账户）
   - `partner_id` = **发起方** memberId
4. **不要混淆 t_acquire_order**：
   - `t_acquire_order` 是商户收单（B2C 支付）
   - `t_deposit_order` 是用户充值（C2 钱包入金）
   - 结构相似，业务不同，查询/统计时务必选对表。
5. **状态与错误码一致性**：失败时 `status` + `fail_code` + `fail_message` + `unity_result_code` 四者要一致，不应出现 status=SUCCESS 但 fail_code 非空的情况。
6. **必填字段校验**：`request_no`、`member_partner_id`、`partner_id`、`member_id`、`product_code`、`currency_code`、`amount`、`qr_code`、`request_time`、`status` 在入库前应校验非空。
7. **下游表一致性**：充值成功后，应能通过 `global_id` 在 `t_payment_info`（必有）、`t_card_info`（卡通道时）、`t_command`（含渠道指令记录）中检索到对应数据。
8. **金额与币种**：`amount` 精度 decimal(19,4)，`currency_code` 必须与下游 payment_info / amount_detail 一致。
9. **幂等**：相同 `request_no` 不应产生多条充值订单，由 `t_request_identity` + 业务唯一约束共同保证。
