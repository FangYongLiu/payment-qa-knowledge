---
title: Jaywan产品Q&A
domain: ppc-card-business
kind: wiki_page
slug: jaywan-product-qa
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:b4ddb781-c8c9-4531-9714-54f78aa19fea
tags: []
---

# Jaywan产品Q&A

本页汇总 Jaywan 预付卡产品侧的常见问答，覆盖虚拟卡申请前置条件、实体卡配送与激活、交易余额查询、以及通知规范等业务问题。完整业务流程参见 [[flow_jaywan_card_lifecycle]]，产品总览见 [[jaywan-prepaid-card-overview]]，相关用例见 [[jaywan-use-case-list]]。

## 虚拟卡

### 申请前置条件
- **客户准入条件**：已完成 Eid KYC、已设置支付密码、已通过身份识别（支付密码或生物识别）。
- **VIP 无 KYC**：Phase 1 不支持。
- **风控限制**：同一 Eid 同一时间仅允许一张卡，无其他限制。
- **是否保存卡号**：是。

### 字段规则
- `CustomerName / CustomerMiddleName / CustomerSurName`：会员系统仅有 full name 与 family name（family name 非必填），具体拆分规则以 PRD 为准。
- 电话号码字段：
  - `TelephoneMasterCountryCode`：国家码示例 971、86。
  - `TelephoneMasterPhoneCode = left(phone number, 3)`。
  - `TelephoneMasterPhone`：手机号剩余部分。
- `ProductNumber`、`SubProductNumber`：在环境配置中设置（gppc-OP-Env Configuration），TODO。

### 关闭卡 & 替换卡
- Dgpay 暂无虚拟卡 replace API。
- 处理方式：调用 close API 后再调用 apply API 完成替换；或等待新的 replace API 上线。
- **不可**直接移除替换卡功能。

### 生命周期
- 虚拟卡生命周期已对齐，详见 [[jaywan-phase1-system-design]]。

## 实体卡

### 配送跟踪 (Delivery Tracking)
- 快递商对接由 Dgpay 负责。
- 状态映射：TODO。

### 卡激活
- 激活时需要身份识别（支付密码或生物识别）。
- 激活前需先完成 PIN 设置。

### 生命周期
- 实体卡生命周期已对齐，详见 [[jaywan-phase1-system-design]]。

## 交易

### 余额查询 (Balance Inquiry)
- 余额不足以支付手续费时是否返回余额：TODO。
- 余额足以支付手续费时：扣费后返回余额。

> 交易相关清算结算细节见 [[jaywan-clearing-settlement-design]]。

## 通知 (Notification)

- SMS 或 BOTIM 通知规范：参考 MasterCard Prepaid Card 的 `ppc-Notifications`，具体规范 TODO。

## 相关链接

- 供应商侧（Dgpay）问答见 [[jaywan-vendor-qa]]。
- Phase 2 相关产品能力（如 Replace Card、Close Card）见 [[jaywan-phase2-system-design]]。
