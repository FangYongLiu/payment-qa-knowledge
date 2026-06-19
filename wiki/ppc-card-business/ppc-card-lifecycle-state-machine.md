---
title: PPC卡生命周期状态机
domain: ppc-card-business
kind: wiki_page
slug: ppc-card-lifecycle-state-machine
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:91e9e034-9e27-4a68-9072-982c0da9e5d5
tags: []
---

# PPC卡生命周期状态机

本页定义 PPC 虚拟卡 / 物理卡 / PIN 的状态枚举、合法与非法转换、配送子状态，作为 AI 推导测试用例（状态覆盖、合法/非法转换、状态依赖前置条件）的结构化依据。

> ⚠️ 当前 enum 不见 `APPLY_FAILED` / `DEACTIVATED` / `SUSPENDED` 等可能存在的状态，待 PPC 后端确认完整 enum + 转换矩阵。

## 虚拟卡状态枚举

来源：`VirtualCardStatus.java`（提取自 ppc-SD-Manually Deactivate Card）

| Code | Name | 中文 | 是否最终态 | UI 展示 |
|---|---|---|---|---|
| A | APPLYING | 申请中 | ❌ | PROCESSING |
| U | UNACTIVATED | 已发卡未激活 | ❌ | UNACTIVATED |
| N | NORMAL | 正常 / 已激活 | ❌ | NORMAL |
| L | LOCKED | 已锁定 | ❌ | LOCKED |
| CI | CLOSING | 关卡中 | ❌ | PROCESSING |
| C | CLOSED | 已关卡 | ✅ | CLOSED |

## 卡产品类型

| Code | Name | 中文 | 允许的身份证件 |
|---|---|---|---|
| MC | MULTI_CURRENCY | 多币种卡 | EID, VIP_EID |
| PR | PAY_ROLL | 工资卡 | EID, PASSPORT, VIP_EID |

- 关闭卡静默批量任务（dormant cleanup）**仅处理 MC 卡**，PR 卡跳过。

## 状态转换表（合法转换）

| from | to | 触发动作 | 前置条件 | 后置动作 |
|---|---|---|---|---|
| (none) | A | 用户申请虚拟卡 | KYC=Tier2，已设置支付密码，同会员同类型卡数量 < 上限 | 创建 `t_virtual_card` 记录，调 YSE/Jaywan 申请 |
| A | U | 卡组织发卡成功通知 | YSE/Jaywan 返回成功 | 推送公众号通知"卡片已就绪" |
| A | (释放) | 申请失败 | 卡组织发卡失败 / 超时 | 释放申请名额 |
| U | N | 用户激活（含 PIN 设置） | 输入正确 ProxyNumber / OTP / KYC 核身 | 推送"卡片已激活" |
| N | L | 用户主动锁卡 / PIN 错误超限（YSE `ResponseCode=75`） | 卡余额可正可负 | 阻止后续授权交易 |
| L | N | 用户解锁 / Reset PIN（调 APIPTR） | 核身通过 | 恢复授权 |
| N / L | CI | 用户主动关卡 / 系统批量停用（dormant） | 卡余额=0；待结算账户已清空；余额同步完成 | 创建关卡订单（`FeeFlag=N`, `Flag=C`, `Amount=0`） |
| CI | C | 卡组织确认关卡 | 关卡订单支付成功 / 订单完成回调 | 推送"卡已关闭" |

## 非法转换（反向用例必出）

| 非法转换 | 风险 | 反向用例 |
|---|---|---|
| C → 任意 | 已销卡的卡仍能操作 = 资损 | 销卡后调激活/锁卡/解锁/查余额/发起授权 → 必须返回 `INVALID_CARD_STATUS` |
| A → N / L / CI / C | 跳过激活直达使用态 | 申请中状态调激活/锁/关卡 → 必须拒绝 |
| U → L / CI | 未激活直接锁/关 | 未激活卡调锁卡接口 → 后端实际允不允需确认；测试断言保持一致 |
| CI → N / L | 关卡中可被恢复 = 资金归属混乱 | 关卡中调激活/解锁 → 必须拒绝 |
| 余额≠0 时关卡 | `DeactivateCardResultCode = NON_ZERO_BALANCE` 跳过停用 | 构造非零余额发起关卡 → 必须返回 `NON_ZERO_BALANCE` |

## 物理卡配送子状态

物理卡配送状态与虚拟卡状态**正交**。基于 4.10.0 release 86 条 Bug 推断：

| 状态 | 含义 | 关键转换触发 |
|---|---|---|
| Preparing your physical card | 已下单制卡中 | 用户支付制卡费成功 |
| Out for delivery | 配送中 | Jeebly API `status=Out for delivery` |
| Delivered | 已送达 | Jeebly API `status=Delivered` |
| Cancelled | 用户取消 | 用户主动取消订单 |
| RTO Delivered | 退回原址 | Jeebly API `status=RTO Delivered` |
| Delivery cancelled | 配送失败 | Jeebly API failure |

- **资损/UX 红线**：`Cancelled` / `RTO Delivered` 后必须**等待 7 天**才能允许重新下物理卡（可配置，参考 WALLET-925）。

## PIN 状态

| PIN 状态 | 触发 | 解除条件 |
|---|---|---|
| Not set | 卡刚激活时 | 用户首次设 PIN |
| Set | 用户设过 PIN | — |
| Locked | 授权 `ResponseCode=75`（连续输错到上限） | 调 APIPTR 重置（Reset PIN） |

## 测试用例生成提示

- **正向状态覆盖（happy path）**：每个合法转换 ≥1 条；6 状态 × 平均 1.5 转换 ≈ 9 条
- **反向状态覆盖（illegal）**：每个非法转换 ≥1 条；销卡后操作类（激活/锁/解锁/查余额/授权）≥5 条
- **并发覆盖**：同卡同时锁/解锁、关卡中再次发起关卡 → 幂等校验
- **配送子状态覆盖**：6 个配送状态 × 关键操作（重新下单、追踪、激活）≥18 条
- **多卡产品差异**：MC vs PR 各自的合法转换 + 静默批量停用规则差异

## 外部参考

- **4 - 状态机（图）** — 含 Physical Card Apply Status 图（图片，需肉眼对照）
- **ppc-SD-Manually Deactivate Card** — 含真实 `VirtualCardStatus` / `DeactivateCardResultCode` enum
- **ppc-系统设计-1-卡管理** — 卡管理总览

## 维护

- **Owner**：Jianfei Wang
- **Backend reviewer**：待 PPC 后端确认完整 enum + 转换矩阵
- **节奏**：卡组织规则变更 / 新 release 时 review，每季度刷新一次
