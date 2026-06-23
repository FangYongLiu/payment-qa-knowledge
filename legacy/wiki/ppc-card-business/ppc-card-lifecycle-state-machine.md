---
title: PPC卡生命周期状态机
domain: ppc-card-business
kind: wiki_page
slug: ppc-card-lifecycle-state-machine
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2133393518
tags: []
---

# PPC卡生命周期状态机

本页结构化定义 PPC 卡的状态、合法/非法转换、配送子状态及 PIN 状态，作为 AI 生成卡相关测试用例的事实基础。配套测试场景见 [[scn_ppc_card_lifecycle_transitions]]。

> ⚠️ 当前 enum 缺少可能存在的 `APPLY_FAILED` / `DEACTIVATED` / `SUSPENDED` 等状态，待 PPC 后端确认完整 enum 与转换矩阵。

## 虚拟卡状态枚举

来源：`VirtualCardStatus.java`（提取自 ppc-SD-Manually Deactivate Card）。

| Code | 名称 | 中文 | 最终态 | UI Summary Status |
|---|---|---|---|---|
| A | APPLYING | 申请中 | ❌ | PROCESSING |
| U | UNACTIVATED | 已发卡未激活 | ❌ | UNACTIVATED |
| N | NORMAL | 正常/已激活 | ❌ | NORMAL |
| L | LOCKED | 已锁定 | ❌ | LOCKED |
| CI | CLOSING | 关卡中 | ❌ | PROCESSING |
| C | CLOSED | 已关卡 | ✅ | CLOSED |

## 卡产品类型

| Code | 名称 | 中文 | 允许的身份证件 |
|---|---|---|---|
| MC | MULTI_CURRENCY | 多币种卡 | EID, VIP_EID |
| PR | PAY_ROLL | 工资卡 | EID, PASSPORT, VIP_EID |

- 关闭卡静默批量任务（dormant cleanup）**仅处理 MC 卡，PR 卡跳过**。

## 状态转换表

| from | to | 触发动作 | 前置条件 | 后置动作 |
|---|---|---|---|---|
| (none) | A | 用户申请虚拟卡 | KYC=Tier2，已设支付密码，同会员同类型卡数 < 上限 | 创建 `t_virtual_card` 记录，调 YSE/Jaywan 申请 |
| A | U | 卡组织发卡成功通知 | YSE/Jaywan 返回成功 | 推送公众号通知"卡片已就绪" |
| A | (申请失败) | 卡组织发卡失败/超时 | — | 释放申请名额 |
| U | N | 用户激活（含 PIN 设置） | ProxyNumber/OTP/KYC 核身正确 | 推送通知"卡片已激活" |
| N | L | 用户主动锁卡 / PIN 错误超限（YSE ResponseCode=75） | 卡余额可正可负 | 阻止后续授权交易 |
| L | N | 用户解锁 / Reset PIN（调 APIPTR） | 核身通过 | 恢复授权 |
| N / L | CI | 用户主动关卡 / 系统批量停用（dormant） | 卡余额=0；待结算账户已清空；余额同步完成 | 创建关卡订单（FeeFlag=N, Flag=C, Amount=0） |
| CI | C | 卡组织确认关卡 | 关卡订单支付成功/订单完成回调 | 推送通知"卡已关闭" |

## 非法转换（反向用例必出）

| 非法转换 | 风险 | 反向用例断言 |
|---|---|---|
| `C` → 任意 | 已销卡仍可操作 = 资损 | 销卡后调激活/锁/解锁/查余额/授权 → 必须返回 `INVALID_CARD_STATUS` |
| `A` → N/L/CI/C | 跳过激活直达使用态 | 申请中调激活/锁/关卡 → 必须拒绝 |
| `U` → L/CI | 未激活直接锁/关 | 未激活卡调锁卡 → 后端实际行为待确认；测试断言保持一致 |
| `CI` → N/L | 关卡中可被恢复 = 资金归属混乱 | 关卡中调激活/解锁 → 必须拒绝 |
| 余额 ≠ 0 时关卡 | 资金未清退 | 构造非零余额发起关卡 → 必须返回 `NON_ZERO_BALANCE`（`DeactivateCardResultCode`） |

## 物理卡配送子状态

物理卡配送状态与虚拟卡状态**正交**。基于 4.10.0 release 86 条 Bug 推断：

| 状态 | 含义 | 关键转换触发 |
|---|---|---|
| Preparing your physical card | 已下单制卡中 | 用户支付制卡费成功 |
| Out for delivery | 配送中 | Jeebly API status=Out for delivery |
| Delivered | 已送达 | Jeebly API status=Delivered |
| Cancelled | 用户取消 | 用户主动取消订单 |
| RTO Delivered | 退回原址 | Jeebly API status=RTO Delivered |
| Delivery cancelled | 配送失败 | Jeebly API failure |

**资损/UX 红线**：`Cancelled` / `RTO Delivered` 后必须等待 **7 天** 才能重新下物理卡（可配置，参考 WALLET-925）。

## PIN 状态

| PIN 状态 | 触发 | 解除条件 |
|---|---|---|
| Not set | 卡刚激活 | 用户首次设 PIN |
| Set | 用户设过 PIN | — |
| Locked | 授权 ResponseCode=75（连续输错到上限） | 调 APIPTR 重置（Reset PIN） |

## 测试用例生成提示

- **正向状态覆盖（happy path）**：每个合法转换 ≥1 条，6 状态 × 平均 1.5 转换 ≈ 9 条
- **反向状态覆盖（illegal）**：每个非法转换 ≥1 条；销卡后操作类 ≥5 条（激活/锁/解锁/查余额/授权）
- **并发覆盖**：同一卡同时锁/解锁、关卡中再次发起关卡 → 幂等校验
- **配送子状态覆盖**：6 个配送状态 × 关键操作（重新下单、追踪、激活）≥18 条
- **多卡产品差异**：MC 与 PR 的合法转换差异 + 静默批量停用规则差异

## 外部参考

- `4 - 状态机（图）` — 含 Physical Card Apply Status 图（图片，需肉眼对照）
- `ppc-SD-Manually Deactivate Card` — 含真实 `VirtualCardStatus` / `DeactivateCardResultCode` enum
- `ppc-系统设计-1-卡管理` — 卡管理总览

## 维护

- **Owner**：Jianfei Wang
- **Backend reviewer**：待 PPC 后端确认完整 enum + 转换矩阵
- **节奏**：卡组织规则变更 / 新 release 时 review，每季度刷新
