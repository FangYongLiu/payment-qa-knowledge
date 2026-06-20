---
id: scn_ppc_card_lifecycle_transitions
object_type: Scenario
domain: ppc-card-business
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:AQ/2133393518
tags:
- ppc
- card-lifecycle
- state-machine
- test-cases
subdomain: card-management
module: card-lifecycle
sensitivity: normal
name: PPC卡生命周期状态转换测试场景集
aliases: []
related_services: []
related_tables:
- t_virtual_card
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
基于 PPC 卡生命周期状态机（[[ppc-card-lifecycle-state-machine]]）推导的测试用例生成场景集，覆盖：
- 正向状态覆盖（happy path）：每个合法转换 ≥1 条用例（6 状态 × 平均 1.5 转换 ≈ 9 条）
- 反向状态覆盖（reverse / illegal）：每个非法转换 ≥1 条；销卡后操作类 ≥5 条
- 并发覆盖：同卡同时锁/解锁、关卡中再次发起关卡（幂等校验）
- 配送子状态覆盖：6 个配送状态 × 关键操作 ≥18 条
- 多卡产品差异：MC 与 PR 各自合法转换 + 静默批量停用规则差异

## 前置条件
- 会员 KYC=Tier2，已设置支付密码
- 同一会员同类型卡数量 < 上限
- 卡产品类型已知（MC=MULTI_CURRENCY / PR=PAY_ROLL）
- 身份证件类型与卡产品匹配：MC 允许 EID/VIP_EID；PR 允许 EID/PASSPORT/VIP_EID
- 关卡前置：卡余额=0、待结算账户已清空、余额同步完成
- 配送子状态测试需依赖 Jeebly API 状态回调

## 操作步骤
**正向用例（合法转换）**
1. 用户申请虚拟卡 → 状态 (无) → A (APPLYING)
2. YSE/Jaywan 返回发卡成功 → A → U (UNACTIVATED)
3. YSE/Jaywan 返回失败 / 超时 → A → (申请失败)，释放申请名额
4. 输入正确 ProxyNumber / OTP / KYC 激活 → U → N (NORMAL)
5. 用户主动锁卡 或 YSE ResponseCode=75 → N → L (LOCKED)
6. 用户解锁 / Reset PIN（调 APIPTR）→ L → N
7. 用户主动关卡 / dormant 批量停用 → N 或 L → CI (CLOSING)
8. 卡组织确认关卡（订单完成回调）→ CI → C (CLOSED)

**反向用例（非法转换）**
1. C → 任意：销卡后调激活/锁卡/解锁/查余额/发起授权（5 条）
2. A → N/L/CI/C：申请中状态调激活/锁/关卡接口
3. U → L/CI：未激活卡调锁卡接口（后端实际行为待确认，断言保持一致）
4. CI → N/L：关卡中调激活/解锁
5. 余额 ≠ 0 时发起关卡

**并发用例**
1. 同一卡同时发起 锁卡 + 解锁
2. 关卡中（CI）再次发起关卡（幂等校验）

**配送子状态用例**（6 状态 × 关键操作：重新下单、追踪、激活）
- Preparing your physical card / Out for delivery / Delivered / Cancelled / RTO Delivered / Delivery cancelled

**多卡产品差异**
1. MC 卡走 dormant cleanup 批量停用
2. PR 卡走 dormant cleanup → 必须跳过

## DB 校验点
- t_virtual_card.status 字段在每次转换后等于目标 enum 值（A/U/N/L/CI/C）
- 关卡订单字段：FeeFlag=N, Flag=C, Amount=0
- 申请失败后申请名额计数已释放
- 销卡后（C）任何写操作不应改变 t_virtual_card 行
- Cancelled / RTO Delivered 后 7 天内重新下物理卡 → 拒绝（参考 WALLET-925 可配置）

## 预期结果
- **正向**：每条合法转换成功，状态字段正确流转，触发对应后置动作（推送通知"卡片已就绪"/"卡片已激活"/"卡已关闭"，调 YSE/Jaywan/APIPTR）
- **反向**：
  - C → 任意操作：返回 `INVALID_CARD_STATUS`
  - A/CI → 激活/解锁/锁卡：必须拒绝
  - 非零余额关卡：返回 `NON_ZERO_BALANCE`（DeactivateCardResultCode）
- **并发**：重复关卡幂等，不产生多笔关卡订单；同时锁/解锁有明确串行结果
- **配送红线**：Cancelled / RTO Delivered 后必须等待 7 天才能重新下物理卡
- **PIN**：授权 ResponseCode=75 触发 PIN Locked，需调 APIPTR Reset PIN 解除
- **产品差异**：dormant cleanup 仅停用 MC 卡，PR 卡跳过
