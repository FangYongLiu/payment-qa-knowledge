---
id: tbl_acquireii_t_terminal_detail
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_terminal_detail.md
tags:
- pos
- 终端
- 门店
subdomain: null
module: null
sensitivity: normal
name: 终端明细表
aliases:
- t_terminal_detail
- acquireii.t_terminal_detail
related_services: []
related_tables:
- tbl_acquire_terminal
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_pay_scene_param
- tbl_acquireii_t_secondary_merchant_detail
related_scenarios:
- scn_fiserv_test_tid_creation
- scn_merchant_transaction_db_check
- scn_payment_code_scanned_by_pos
- scn_payment_code_scanned_by_scanner
related_logs: []
related_requirements: []
related_failures: []
---

## 用途与定位

`acquireii.t_terminal_detail`（终端明细表）用于记录一笔收单订单来自**哪个终端 / 门店 / 操作员**，是 POS、门店收银等线下场景的核心补充信息表。

在收单交易链路中：
- 主表 `t_acquire_order` 承载订单主体信息；
- 当订单来源为 POS / 门店收银等终端场景时，会同步落一条 `t_terminal_detail`，与主表通过 `global_id` 形成 **1:1 关联**；
- 线上 / 纯渠道订单一般**不会**写本表。

常见使用场景：付款码被 POS 机扫、付款码被扫码枪扫、Fiserv TID 测试构造、商户交易落库校验等。

## 关键字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `global_id` | bigint | 主键，对应 `t_acquire_order.global_id` |
| `operator_id` | varchar(200) | 操作员 ID（收银员），用于审计追溯 |
| `terminal_id` | varchar(200) | 终端 ID（POS 设备号） |
| `terminal_type` | varchar(50) | 终端类型 |
| `store_id` | varchar(200) | 门店 ID |
| `store_name` | varchar(200) | 门店名 |
| `merchant_name` | varchar(200) | 商户名 |
| `location` | varchar(200) | 位置信息 |

## 主键 / 索引

- PRIMARY：`global_id`
- `i_td_t`：`terminal_id`，按终端维度查询
- `i_td_str`：`store_id`，按门店维度查询

## 与其他表的关系

| 关联表 | 关联键 | 关系 | 说明 |
|--------|--------|------|------|
| `t_acquire_order` | `global_id` | 1:1 | 订单主表，POS 场景下必有对应明细 |
| `t_acquire_terminal` (`tbl_acquire_terminal`) | `terminal_id` | N:1 | 终端档案表；`t_terminal_detail.terminal_id` 必须能在终端档案中找到，且为同一个 ID |
| `t_pay_scene_param` | `global_id` | 1:1 | 支付场景参数；POS 扫码场景需联合判断 scene 是否一致 |
| `t_secondary_merchant_detail` | `global_id` | 1:1 | 二级商户明细，门店/商户名可能交叉校对 |

## QA 落库检查要点

1. **场景判断优先**：仅 POS / 线下终端场景才有记录。线上订单缺失本表属正常，**校验脚本不要默认 SELECT 必有结果**，需先按订单场景分支。
2. **1:1 关联完整性**：按 `global_id` 关联 `t_acquire_order`，应有且仅有 1 条；出现 0 条（POS 场景）或 >1 条均为异常。
3. **terminal_id 一致性**：`t_terminal_detail.terminal_id` 必须等于 `t_acquire_terminal.terminal_id`，并能在终端档案表中查到对应启用记录。
4. **operator_id 审计字段**：用于门店收银员追溯，QA 用例中如指定收银员，需校验落库值与请求一致。
5. **门店信息一致性**：`store_id` / `store_name` / `merchant_name` 与商户配置 / 二级商户明细中的对应值保持一致，不应出现拼写或编码差异。
6. **索引命中**：按终端、按门店的查询用例，确认走 `i_td_t` / `i_td_str` 索引。
7. **付款码扫码方向**：付款码被 POS / 扫码枪扫两种场景下，`terminal_type` 取值需符合该场景的约定枚举。