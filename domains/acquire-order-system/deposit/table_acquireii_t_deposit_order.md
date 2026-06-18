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
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

记录用户向钱包/账户**充值（deposit）**的订单数据。和 `t_acquire_order`（商户收单 B2C 支付）业务结构相似但场景不同，本表面向 C2 钱包入金。

典型场景：
- 用户在 Kiosk（自助终端）扫码充值
- 用户向自己的 Wallet 入金
- 用户向特定 QR 码（如商家收款码）充值

表名 `acquireii.t_deposit_order`，主键 `global_id`，重要程度 ⭐⭐⭐⭐。

## 关键列

**主键和标识**
- `global_id` bigint：主键，全局号
- `request_no` varchar(200)：等同于 requestIdentity.requestNo
- `voucher_no` varchar(200)：凭证号

**业务方信息**
- `member_partner_id` varchar(200)：memberPartnerId
- `partner_id` varchar(200)：发起方 memberId
- `member_id` varchar(200)：收款人 mid（充值目标钱包/账户）
- `product_code` varchar(200)：产品码

**充值金额**
- `currency_code` varchar(50)：充值币种
- `amount` decimal(19,4)：充值金额
- `qr_code` varchar(200)：二维码（唯一约束）

**业务信息**
- `subject` varchar(200)：标题
- `notify_url` varchar(500)：通知地址
- `request_time` timestamp(3)：请求时间
- `inst_code` varchar(32)：机构代码
- `kiosk_id` varchar(100)：Kiosk 设备 ID（非 Kiosk 充值为 NULL）

**状态机**
- `status` varchar(200)：充值订单状态
- `fail_code` varchar(50)：错误码
- `fail_message` varchar(200)：错误描述
- `unity_result_code` varchar(200)：统一结果码

**时间和版本**
- `created_time`、`last_updated_time` timestamp(3)
- `data_version` bigint：数据版本

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `global_id` | 主键 |
| `ui_t_d_o_qr_code` | `qr_code` | 唯一约束（一个 QR 码对应一笔订单） |
| `i_ao_ct` | `created_time` | 按时间查 |
| `i_ao_lut` | `last_updated_time` | 按更新时间扫 |

通过 `global_id` 可关联：支付完成信息 `t_payment_info`、卡支付信息 `t_card_info`、指令调度 `t_command`。

## 校验点(QA 关注)

1. **qr_code 唯一约束**：同一个 QR 码不能创建两笔订单，重复创建应被唯一索引拦截。
2. **kiosk_id 区分场景**：Kiosk 充值场景该字段必填，非 Kiosk 充值为 NULL；做 Kiosk 统计时需按 `kiosk_id IS NOT NULL` 过滤。
3. **member_id 语义**：本表 `member_id` 是**收款人**（充值目标），`partner_id` 是发起方 memberId，不要弄反。
4. **不要混淆 t_acquire_order**：t_acquire_order 是商户收单（B2C 支付），t_deposit_order 是用户充值（C2 钱包入金），结构相似但业务不同，查询/统计时注意选对表。
5. **状态与错误码**：失败时关注 `status` + `fail_code`/`fail_message`/`unity_result_code` 三者一致性。
6. **必填字段**：`request_no`、`member_partner_id`、`partner_id`、`member_id`、`product_code`、`currency_code`、`amount`、`qr_code`、`request_time`、`status` 等必填，缺失应在入库前校验。
