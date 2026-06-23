---
title: Jaywan-Dgpay对接集成指南
domain: ppc-card-business
kind: wiki_page
slug: jaywan-dgpay-integration-guide
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/877428845
tags: []
---

# Jaywan-Dgpay对接集成指南

本页汇总 Botim/Astratech 与 Dgpay 之间的 API 对接规范，包括通用调用方式、Token 管理、加解密机制，以及 Institution 侧需实现的反向 API。业务背景与端到端流程见 [[jaywan-prepaid-card-overview]]，详细排期见 [[jaywan-system-design-phases]]。

## API 调用通用规范

- 协议：HTTP，请求/响应均为 JSON 格式。
- 鉴权：在 HTTP Header 中携带 token，格式示例：
  - `Authorization: NWZhMDYwYjAtYjQyZS00OWRhLWE2NmUtNTgxNjM1N2YxMTJi`
- 通用封装要求（内部实现）：
  - Vendor 方向：简化通用请求流程，统一 token 拼接与 POJO 转换；单元测试中 mock vendor responder。
  - Institution 方向：简化通用响应流程，统一 token 校验与 POJO 转换；单元测试中 mock vendor requester。

## Vendor 侧 API 一览（调用 Dgpay）

| 用例 | Dgpay API |
|---|---|
| 通用调用 | GetToken |
| 创建虚拟卡 | CreatePrepaidDigitalCard（错误恢复用 GetPrepaidCards） |
| 查看卡详情 | GetPrepaidCardInfo |
| 锁卡/解锁/换卡/销卡 | UpdatePrepaidCardStatus |
| Reset PIN | PrepaidCardPinOperation |
| 申请实体卡 | CreatePrepaidEmbossData |
| 激活实体卡 | ActivatePrepaidCard |
| 手机号同步 | UpdateMobilePhoneNumber |
| Bank Portal 批量开卡 | NotifyPrintedCards |
| 短信服务 | SMS Service（当前无使用场景） |

## Institution 反向 API 一览（Dgpay 调用我方）

我方需实现一套与 Dgpay 对称的接口，供其反向调用。

| 用例 | Institution API |
|---|---|
| 获取 Token | get-token |
| 交易（Provision） | provision |
| 交易冲正 | reversal |
| 余额查询 | balance-inquiry |
| 拒绝交易通知 | declined-transaction |
| 银行后台更新卡状态 | update-prepaid-card-status |
| 物流轨迹通知 | notify-courier-process |

## Token 管理

### Vendor Token（我方调用 Dgpay）

- 通过 `GetToken` 申请并管理。
- Dgpay 生成的 token 会被持久化，不受系统重启或其他操作事件影响。
- 在旧 token 过期前异步生成新 token，避免业务中断。

### Institution Token（Dgpay 调用我方）

- 我方需实现与 Dgpay 对称的 `get-token` 接口，自行生成并管理 institution token。
- 反向请求进入时统一做 token 校验。

## 加解密机制

### 密钥交换

- 双方互换公钥：我方将公钥共享给 Dgpay，Dgpay 也将公钥共享给我方。
- 请求中需加密的敏感数据（我方→Dgpay）：使用 Dgpay 公钥加密，例如 PIN 设置时的 PIN 值。
- 响应中需加密的敏感数据（Dgpay→我方）：使用我方公钥加密，例如 `createCard`、`getPrepaidCardInfo` 等方法返回的卡号与 CVV2，由我方解密。
- 加密密钥无指定有效期。

### 内部实现

- 提供内部 API 用于获取密钥。
- 提供加解密 API。
- 加解密流程详见 wiki：gppc-OP-Key Generation。

## 字段与配置约定

- 姓名拆分：会员系统仅有 full name 与 family name（非必填），与 Dgpay 的 `CustomerName / CustomerMiddleName / CustomerSurName` 的映射规则以 PRD 为准。
- 电话字段拆分规则：
  - `TelephoneMasterCountryCode`：示例 `971`、`86`
  - `TelephoneMasterPhoneCode = left(phone number, 3)`
  - `TelephoneMasterPhone`：剩余部分
- `ProductNumber`、`SubProductNumber` 配置：见 gppc-OP-Env Configuration（待补）。

## 关键调用与错误恢复

### CreatePrepaidDigitalCard 超时恢复

- 若 `CreatePrepaidDigitalCard` 调用读超时、无法确认是否建卡成功：
  - 调用 `GetPrepaidCards`（或 GetDebitCardList）拉取该客户全部卡片列表。
  - 与钱包侧本地卡列表比对，识别"超时但实际已创建"的卡。
  - 处理方式二选一：将新增卡保存入库，或通过 `UpdatePrepaidCardStatus` 关闭该卡。

### 换卡（Replace Card）

- Dgpay 当前 `ReplaceCard` 以 emboss 信息为入参，常规仅用于实体卡。
- 虚拟卡换卡的实现方式：先用 `UpdatePrepaidCardStatus` 关闭原卡，再调 `CreatePrepaidDigitalCard` 申请新卡（与 replacement 流程等价）；或等待 Dgpay 提供新的 replace API。

### 余额同步

- 若 Botim 持有余额：请求为 pass-through，无需 `UpdateCardBalance` 同步。
- 若 mBank 持有余额：需要余额同步；但当前结论是 Dgpay 侧不维护余额，因此**无需余额同步**。
- `UpdateCardBalance` 是覆盖式更新而非增减，存在并发不一致风险，不在本期使用。

## Institution 反向 API 实现要点

- **provision**：实现 provision 报文处理；集成风控、支付、账单、PNS；覆盖交易与退款。
- **balance-inquiry**：实现余额查询报文；新增余额查询能力。
- **reversal**：实现冲正报文；包含额外的重试流程；与单笔报文交易的冲正结算更新对接。
- **declined-transaction**：保存被拒交易；按需要发送通知。
- **update-prepaid-card-status**：处理银行后台发起的卡状态变更。
  - 注意：若 institution 响应失败，Dgpay 侧状态是否更新待确认（TODO）。
- **notify-courier-process**：实体卡物流轨迹回调；`CardProcessStatusID` / `CardProcessSubStatusID` 枚举值待 Dgpay 提供（TODO）。

## 相关链接

- 业务问题与产品规则：[[jaywan-product-qa]]
- 供应商接口疑问：[[jaywan-vendor-qa]]
- 清算与结算文件对接：[[jaywan-clearing-settlement-design]]
- 业务域：[[domain_jaywan_prepaid_card]]
