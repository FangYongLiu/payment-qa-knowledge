---
id: tbl_acquireii_t_acquire_order
object_type: Table
domain: acquire-transaction
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_acquire_order.md
tags:
- acquireii
- 收单
- 订单主表
- 核心表
subdomain: null
module: null
sensitivity: normal
name: 收单订单主表 t_acquire_order
aliases:
- t_acquire_order
- acquireii.t_acquire_order
related_services: []
related_tables:
- tbl_acquireii_t_amount_detail
- tbl_acquireii_t_card_info
- tbl_acquireii_t_command
- tbl_acquireii_t_dcc_info
- tbl_acquireii_t_deposit_order
- tbl_acquireii_t_goods_detail
- tbl_acquireii_t_pay_scene_param
- tbl_acquireii_t_payment_info
- tbl_acquireii_t_preauth_control
- tbl_acquireii_t_preauth_relation
- tbl_acquireii_t_promotion_info
- tbl_acquireii_t_refund_order
- tbl_acquireii_t_request_identity
- tbl_acquireii_t_retryable_command
- tbl_acquireii_t_reversal_order
- tbl_acquireii_t_reversal_orderii
- tbl_acquireii_t_revoke_order
- tbl_acquireii_t_secondary_merchant_detail
- tbl_acquireii_t_sharing_info
- tbl_acquireii_t_stmt_event
- tbl_acquireii_t_terminal_detail
- tbl_acquireii_t_unretryable_command
- tbl_acquireii_t_void_ops_order
- tbl_acquireii_t_void_order
related_scenarios:
- scn_acquire_product_apply
- scn_cko_standalone_card_binding
- scn_cko_subscription_test_cards
- scn_fiserv_test_tid_creation
- scn_merchant_transaction_db_check
- scn_mit_autodebit
- scn_mit_cit_directpay_first
- scn_mit_cit_directpay_subsequent
- scn_mit_cit_payandsign
- scn_mit_cit_test_guide
- scn_payment_code_scanned_by_pos
- scn_payment_code_scanned_by_scanner
related_logs: []
related_requirements: []
related_failures: []
---

## 用途与定位

`acquireii.t_acquire_order`(收单订单主表) 是 acquireii 库**最核心**的表,承载商户发起的**所有收单交易订单**主数据。一笔订单从下单 → 支付 → 完成的全流程,主表数据都落在这里。

表注释：收单数据。重要程度 ⭐⭐⭐⭐⭐。

### 在交易链路中的位置

```
商户调用 placeOrder
      │
      ▼
[t_request_identity] ── request_no 幂等 ──┐
      │                                   │
      ▼                                   │
[t_acquire_order] ◄────── 主订单(本表) ◄──┘
   │ global_id 关联
   ├── t_card_info / t_payment_info / t_amount_detail / t_dcc_info
   ├── t_terminal_detail / t_goods_detail / t_pay_scene_param
   ├── t_secondary_merchant_detail / t_sharing_info / t_promotion_info
   │
   │ acquire_global_id 关联
   ├── t_refund_order   (退款,1:N)
   ├── t_void_order / t_void_ops_order (撤销,1:N)
   └── t_reversal_order / t_reversal_orderii / t_revoke_order (冲正)
      │
      ▼
[t_command / t_retryable_command / t_unretryable_command] —— 异步指令驱动状态流转
      │
      ▼
[t_stmt_event] —— 对账事件
```

典型场景：
- 商户调用 `placeOrder` 接口创建支付订单 → 写入一条记录
- 用户支付完成 → status 流转
- 查询订单状态 → 主要从这张表查
- 退款 / 撤销 / 冲正 → 都通过 global_id 关联回这张表

## 关键列

### 主键和标识
- `global_id` (bigint, 必填)：主键,全局唯一订单号,**所有子表的外键基准**
- `request_no` (varchar(200), 必填)：等同于 requestIdentity.requestNo,用于幂等防重和查询
- `voucher_no` (varchar(200))：凭证号
- `mis_order_no` (varchar(128))：mis 系统订单号(外部对接)
- `receipt_no` (varchar(50))：receipt 编号

### 业务方信息
- `partner_id` (varchar(200), 必填)：发起方商户 memberId(最常查询字段)
- `device_id` (varchar(200))：发起方设备 ID(POS 等场景)
- `payee_mid` (varchar(200), 必填)：收款人 mid
- `secondary_merchant_id` (varchar(64))：二级商户号
- `multi_merchant_name` (varchar(50))：收款方名字

### 订单信息
- `product_code` (varchar(200), 必填)：产品码(区分业务类型)
- `ttlamt_currency_code` (varchar(50))：币种代码
- `total_amount` (decimal(19,4))：收单金额
- `subject` / `subject_ar` (varchar(200))：订单标题 / 阿拉伯语标题
- `expired_time` (timestamp(3), 必填)：订单过期时间
- `notify_url` (varchar(500))：商户回调通知地址
- `acquire_order_usage` (varchar(64))：收单类型

### 支付场景
- `pay_scene_code` (varchar(32), 必填)：支付场景代码(PAYPAGE / DEEPLINK / ONETIME 等)
- `trade_routing` (varchar(50))：交易路由

### 状态机
- `status` (varchar(200), 必填)：订单状态(核心字段)
- `fail_code` / `fail_message`：失败错误码 / 描述
- `unity_result_code` (varchar(200))：统一结果码
- `request_time` (timestamp(3), 必填)：商户声明请求时间

### 撤销 / 冲正标记
- `revoked` (varchar(8))：是否冲正(Y/N)
- `reversal` (varchar(8))：是否 reversal(Y/N)
- `revoke_type` (varchar(16))：冲正类型

### 其他
- `reserved` (varchar(200))：预留字段
- `created_time` / `last_updated_time` (timestamp(3), 必填)：创建/更新时间
- `data_version` (bigint, 必填)：数据版本号(乐观锁)

## 主键 / 索引

- PRIMARY: `global_id`
- `i_ao_ct`：created_time —— 按创建时间查询
- `i_ao_pid_ct`：partner_id, created_time —— **最常用**：按商户 + 时间范围查
- `i_ao_py_ct`：payee_mid, created_time —— 按收款方 + 时间查
- `i_ao_rn`：request_no —— 按 request_no 查(幂等防重)
- `i_ao_rcn`：receipt_no —— 按 receipt_no 查
- `i_ao_resv`：reserved(20) —— 按 reserved 前缀查
- `idx_up_status`：last_updated_time, status —— 状态扫描类查询

常用查询模式：
- 按 `global_id` 查单笔
- 按 `request_no` 查(防重)
- 按 `partner_id + created_time` 范围查(商户报表)

## 关联表关系

### 通过 `global_id` 关联(同一笔订单的明细)
| 关联表 | 关系 | 说明 |
|---|---|---|
| `t_card_info` | 1:1 | 支付卡信息 |
| `t_payment_info` | 1:1 | 支付信息(渠道、流水等) |
| `t_amount_detail` | 1:1 | 金额明细(手续费、税等) |
| `t_dcc_info` | 1:1 | DCC 货币转换 |
| `t_terminal_detail` | 1:1 | 终端明细(POS) |
| `t_goods_detail` | 1:N | 商品明细 |
| `t_pay_scene_param` | 1:N | 支付场景参数 |
| `t_secondary_merchant_detail` | 1:1 | 二级商户明细 |
| `t_pcc_content` | 1:1 | PCC 内容 |
| `t_sharing_info` | 1:N | 分账信息 |
| `t_promotion_info` | 1:N | 优惠券信息 |

### 通过 `acquire_global_id` 关联(后续操作)
| 关联表 | 关系 | 说明 |
|---|---|---|
| `t_refund_order` | 1:N | 退款订单 |
| `t_void_order` | 1:N | 撤销订单 |
| `t_void_ops_order` | 1:N | 运营撤销订单 |
| `t_reversal_order` / `t_reversal_orderii` | 1:N | Reversal 订单 |
| `t_revoke_order` | 1:N | 冲正订单 |
| `t_preauth_relation` | 1:N | 预授权关系(预授权场景) |

### 通过 `request_no` 关联
- `t_request_identity`(1:1) —— 幂等校验源头

### 间接关联
- `t_command` / `t_retryable_command` / `t_unretryable_command` —— 异步指令,驱动 status 变化
- `t_stmt_event` —— 对账事件

## QA 落库检查要点

1. **不要做不带索引的全表扫描**：表数据量极大(千万级以上),查询必须带索引字段(优先 `global_id` / `request_no` / `partner_id+created_time`)。
2. **状态流转复杂**：status 可能值需要参考代码或业务文档,落库检查应明确预期 status 值。
3. **partner_id 是商户 memberId**,不是 `secondary_merchant_id`,校验时不要混淆。
4. **revoked / reversal 是冗余标记**：仅记录是否被撤销/冲正,实际撤销/冲正订单在 `t_void_order` / `t_reversal_order` / `t_revoke_order`,对账要从对应表取数据。
5. **subject_ar 是阿拉伯语标题**,本地化(中东)场景下不能为空。
6. **时间字段语义**：`request_time` 是商户声明的时间,**不是入库时间**;入库时间用 `created_time`,不能错用。
7. **request_no 是幂等核心**：同一 request_no 不允许重复落单,验证幂等需查 `i_ao_rn` 索引及 `t_request_identity`。
8. **data_version 为乐观锁**：状态更新需基于版本号,避免并发覆盖,QA 验证并发场景必须关注此字段递增。
9. **expired_time 必填**：过期后订单不应继续支付,需验证状态流转是否拒绝过期单。
10. **子表一致性校验**：`global_id` 在主表落库后,关联子表(card_info / payment_info / amount_detail 等)是否按场景齐全,金额、币种、商户 ID 在主子表间是否一致。
11. **撤销/退款链路验证**：发起 void/refund/reversal 后,需同时检查本表对应标记字段(`revoked`/`reversal`)与子表记录是否对应。
