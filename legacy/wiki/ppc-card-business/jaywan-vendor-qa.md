---
title: Jaywan供应商(Dgpay)Q&A
domain: ppc-card-business
kind: wiki_page
slug: jaywan-vendor-qa
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/877428845
tags: []
---

# Jaywan供应商(Dgpay)Q&A

汇总与 Dgpay 在通用调用、虚拟卡、实体卡、卡管理、余额同步、对账结算等方面的对接澄清。相关上下游参考 [[jaywan-product-qa]] 与 [[jaywan-dgpay-integration-guide]]。

## Common

### 调用样例与定义
- 协议：HTTP，请求/响应均为 JSON 格式
- 鉴权：Token 放在 HTTP Header，例如 `Authorization: NWZhMDYwYjAtYjQyZS00OWRhLWE2NmUtNTgxNjM1N2YxMTJi`

### API - GetToken
- Dgpay 生成的 token 会被持久化，不受系统重启或其他运行事件影响
- Institution 需实现同名/对等的 token 接口，以便 Dgpay 反向调用本侧

### Encrypt & Decrypt
- 公钥互换：双方各自共享公钥
  - 我方使用 Dgpay 的公钥加密 PIN（如 PIN set 场景）
  - Dgpay 使用我方公钥加密敏感数据（如 createCard、getPrepaidCardInfo 输出中的卡号、CVV2），由我方解密
- 加密密钥无指定有效期

### API - SMS Service
- 当前不使用；交易 OTP 也不通过该 API 发送

## Virtual Card

### API - CreateDigitalCard
- 超时恢复：当 `CreateDigitalCard` 读超时、无法确认是否创建成功时，可调用 `GetDebitCardList`（即 `GetPrepaidCards`）拉取该客户全部卡片
  - 与本地卡片列表比对，发现多出的卡即为超时但已创建的卡
  - 处理方式：保存到本地系统，或通过 `UpdateDebitCardStatus` 关闭该卡
  - 也可与 Dgpay 讨论其他恢复流程
- 推荐错误恢复 API：`GetPrepaidCards`

### Card Status Update Service
- 若 institution 响应失败，Dgpay 侧状态是否回滚 → TODO

## Physical Card

### API - NotifyPrintedCards
- 用途：Bank portal 批量 onboarding

### API - Courier Notification Service
- `CardProcessStatusID`、`CardProcessSubStatusID` 的枚举值 → TODO

### Card PIN
- PIN 使用场景：实体卡为主，亦可能用于 tap pay

## Card Management

### Replace Card
- `ReplaceCard` 方法以 emboss 信息为输入，通常只适用于实体卡
- 若需对数字卡换卡，两种方式：
  1. 由 Dgpay 扩展支持数字卡 ReplaceCard
  2. 先通过 `UpdateDebitCardStatus` 关闭原数字卡，再调用 `createDigitalCard` 重新申请（流程等同 replacement）

## Balance sync

### API - UpdateCardBalance
- 该接口为"替换式"更新（覆盖余额而非增减），并发场景下存在不一致风险
- 结论：Dgpay 侧不维护余额，无需余额同步
  - 若 Botim 持有余额，请求即透传，无需此 section
  - 若 Mbank 持有余额，则需要余额同步

## Reconciliation & Settlement
- Settlement：由 Mbank 与 Botim 共同管理
- Reconciliation：由 Botim 负责
- 若余额由 Botim 持有，SWITCH 到 host 的对账活动也由 Botim 完成
- Settlement 与 clearing 的报表/格式将由 Mbank 侧共享给 Botim
- 详细方案见 [[jaywan-clearing-settlement-design]]

## Other

### KYC
- 是否需要传 KYC 信息给 Dgpay 以启用 Jaywan 卡：需要
- 依据：CBUAE 要求银行在 banking-as-a-service 场景下完成 KYC 与 KYCC
- 待 Botim 明确所需 KYC 字段，以及仅校验还是需要存储

### Chargeback
- Botim 将 chargeback 详情与客户签署文件以 form/email 模板发送给 Mbank
- 由 Mbank 通过 CBUAE portal 发起 chargeback

### Dashboard
- 可根据 Botim 需求定制

---
所属业务域：[[domain_jaywan_prepaid_card]]
