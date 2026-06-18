---
id: tbl_acquireii_t_acquire_order
object_type: Table
domain: acquireii-core
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
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_acquire_order` 是 acquireii 库最核心的表，承载商户发起的**所有收单交易订单**。一笔订单从下单 → 支付 → 完成的全流程，主表数据都落在这里。

典型场景：
- 商户调用 `placeOrder` 接口创建支付订单 → 写入一条记录
- 用户支付完成 → status 流转
- 查询订单状态 → 主要从这张表查
- 退款 / 撤销 / 冲正 → 都通过 global_id 关联回这张表

表注释：收单数据。重要程度 ⭐⭐⭐⭐⭐。

## 关键列

**主键和标识**
- `global_id` (bigint, 必填)：主键，全局唯一订单号
- `request_no` (varchar(200), 必填)：等同于 requestIdentity.requestNo，用于幂等防重和查询
- `voucher_no` (varchar(200))：凭证号
- `mis_order_no` (varchar(128))：mis 系统订单号（外部对接）
- `receipt_no` (varchar(50))：receipt 编号

**业务方信息**
- `partner_id` (varchar(200), 必填)：发起方商户 memberId（最常查询字段）
- `device_id` (varchar(200))：发起方设备 ID（POS 等场景）
- `payee_mid` (varchar(200), 必填)：收款人 mid
- `secondary_merchant_id` (varchar(64))：二级商户号
- `multi_merchant_name` (varchar(50))：收款方名字

**订单信息**
- `product_code` (varchar(200), 必填)：产品码（区分业务类型）
- `ttlamt_currency_code` (varchar(50))：币种代码
- `total_amount` (decimal(19,4))：收单金额
- `subject` / `subject_ar` (varchar(200))：订单标题 / 阿拉伯语标题
- `expired_time` (timestamp(3), 必填)：订单过期时间
- `notify_url` (varchar(500))：商户回调通知地址
- `acquire_order_usage` (varchar(64))：收单类型

**支付场景**
- `pay_scene_code` (varchar(32), 必填)：支付场景代码（PAYPAGE / DEEPLINK / ONETIME 等）
- `trade_routing` (varchar(50))：交易路由

**状态机**
- `status` (varchar(200), 必填)：订单状态（核心字段）
- `fail_code` / `fail_message`：失败错误码 / 描述
- `unity_result_code` (varchar(200))：统一结果码
- `request_time` (timestamp(3), 必填)：商户声明请求时间

**撤销 / 冲正标记**
- `revoked` (varchar(8))：是否冲正（Y/N）
- `reversal` (varchar(8))：是否 reversal（Y/N）
- `revoke_type` (varchar(16))：冲正类型

**其他**
- `reserved` (varchar(200))：预留字段
- `created_time` / `last_updated_time` (timestamp(3), 必填)：创建/更新时间
- `data_version` (bigint, 必填)：数据版本号（乐观锁）

## 主键/索引

- PRIMARY: `global_id`
- `i_ao_ct`：created_time，按创建时间查询
- `i_ao_pid_ct`：partner_id, created_time —— **最常用**：按商户 + 时间范围查
- `i_ao_py_ct`：payee_mid, created_time，按收款方 + 时间查
- `i_ao_rn`：request_no，按 request_no 查（幂等防重）
- `i_ao_rcn`：receipt_no，按 receipt_no 查
- `i_ao_resv`：reserved(20)，按 reserved 前缀查
- `idx_up_status`：last_updated_time, status，状态扫描类查询

常用查询模式：
- 按 `global_id` 查单笔
- 按 `request_no` 查（防重）
- 按 `partner_id + created_time` 范围查（商户报表）

**关联关系**：
- 通过 `global_id` 关联：`t_card_info`(1:1)、`t_amount_detail`(1:1)、`t_goods_detail`(1:N)、`t_terminal_detail`(1:1)、`t_payment_info`(1:1)、`t_dcc_info`(1:1)、`t_pay_scene_param`(1:N)、`t_pcc_content`(1:1)、`t_secondary_merchant_detail`(1:1)
- 通过 `acquire_global_id` 关联：`t_refund_order`(1:N)、`t_void_order`(1:N)、`t_void_ops_order`(1:N)
- 通过 `request_no` 关联：`t_request_identity`(1:1)

## 校验点(QA 关注)

1. **不要做不带索引的全表扫描**：表数据量极大（千万级以上），查询必须带索引字段。
2. **状态流转复杂**：status 可能值需要参考代码或业务文档。
3. **partner_id 是商户 memberId**，不是 secondary_merchant_id，校验时不要混淆。
4. **revoked / reversal 是冗余字段**：仅记录是否被撤销/冲正，实际撤销订单在 `t_void_order` / `t_reversal_order`，对账要从对应表取数据。
5. **subject_ar 是阿拉伯语标题**，本地化场景下不能为空。
6. **request_time 是商户声明的时间**，不是入库时间；入库时间用 `created_time`，时间字段语义不能错用。
7. **request_no 是幂等核心**：同一 request_no 不允许重复落单，验证幂等需查 `i_ao_rn` 索引及 `t_request_identity`。
8. **data_version 为乐观锁**：状态更新需基于版本号，避免并发覆盖。
9. **expired_time 必填**：过期后订单不应继续支付，需验证状态流转是否拒绝过期单。
