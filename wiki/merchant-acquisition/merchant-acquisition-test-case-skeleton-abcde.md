---
title: 标准用例骨架 A/B/C/D/E
domain: merchant-acquisition
kind: wiki_page
slug: merchant-acquisition-test-case-skeleton-abcde
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:4ef3640b-38b5-4756-81d5-d729c241dc79
tags: []
---

# 标准用例骨架 A/B/C/D/E

每个商户收单场景至少要覆盖以下 5 类用例（A/B/C/D/E）。这是场景手册（§5.x）编写用例库时的最小覆盖面，配合 [[merchant-acquisition-e2e-five-stage-verification]] 的五段式验证一起用。

## A 组：正向流程（Happy Path）

每个场景最少 3-5 条：

- **A1**：标准成功路径
- **A2**：不同卡品牌 / 不同支付方式（Local / International / MasterCard / Visa / ApplePay / GooglePay / SamsungPay）
- **A3**：不同金额（< 100、= 100、> 100，注意 ≥500 触发密码验证）
- **A4**：存卡（saveCard / cardToken 复用）
- **A5**：异步通知 + 对账单生成

## B 组：异常流程（Negative Path）

- **B1**：参数缺失 / 非法（每个必填字段都测一遍 missing 和 invalid）
- **B2**：内部 API 超时 / 异常
- **B3**：外部渠道错误（用 MPGS 特殊 expiry 模拟）：
  - `01/39 APPROVED`（成功）
  - `05/39 DECLINED`
  - `04/27 EXPIRED_CARD`
  - `08/28 TIMED_OUT`
  - `01/37 ACQUIRER_SYSTEM_ERROR`
  - `02/37 UNSPECIFIED_FAILURE`
  - `05/37 UNKNOWN`
- **B4**：风控拒绝（如金额 = 1,000,000 触发限额）
- **B5**：重复请求 / 幂等冲突

错误码对照见 [[merchant-acquisition-error-code-quickref]]，特殊 expiry 触发卡号见 [[merchant-acquisition-test-data-conventions]]。

## C 组：数据一致性（Consistency）

- **C1**：端到端落库验证（按五段式段 ③ 全表核对）
- **C2**：Fund Flow 借贷平衡（按五段式段 ④，Total Dr = Total Cr）
- **C3**：跨表关联字段一致（`merchantOrderNo` / `paymentSeqNo` / `preauthOrderNo`）
- **C4**：对账单生成与订单数据一致

详细的落库表清单与 Fund Flow 校验方法见 [[merchant-acquisition-e2e-five-stage-verification]]，对账文件结构见 [[merchant-acquisition-notify-and-statement]]。

## D 组：边界与并发（Boundary & Concurrency）

- **D1**：金额边界（0 / 0.01 / 上限 9,999,999.99）
- **D2**：时间戳边界（±15 分钟）
- **D3**：同一 `merchantOrderNo` 高并发下单 → 验证幂等
- **D4**：跨日订单（23:59 创建，0:01 通知）
- **D5**：长字符串 / 特殊字符 / 多语言字符

## E 组：权限与安全（Auth & Security）

- **E1**：商户未开通对应产品包 → 验证 `62026 PRODUCT_IS_NOT_APPLIED`
- **E2**：跨商户使用资源（cardToken、preauthOrderNo） → 验证 `Invalid partner id`
- **E3**：签名错误 / Partner-Id 错误 → `403 UNAUTHORIZED`
- **E4**：时间戳超 15 分钟 → `400 REQUESTTIME_TOO_EARLY/LATER`
- **E5**：IP 白名单不在范围 → 拒绝

## 与场景手册的关系

- 每个 §5.x 场景手册都按 A/B/C/D/E 五组扩展为具体用例库
- 每条用例的执行都要走完 [[merchant-acquisition-per-transaction-checklist]]
- 用例所需的卡号、金额、merchantOrderNo 命名见 [[merchant-acquisition-test-data-conventions]]
- 调用模板见 [[merchant-acquisition-curl-postman-skeleton]]
- 整体方法论回到 [[merchant-acquisition-test-methodology-overview]]
