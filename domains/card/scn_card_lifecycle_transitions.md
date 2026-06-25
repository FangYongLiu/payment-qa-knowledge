---
id: scn_card_lifecycle_transitions
object_type: Scenario
name: PPC 卡生命周期状态转换测试场景集
aliases: [卡生命周期状态机, card lifecycle state machine, PPC card lifecycle transitions]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2133393518 (PPC 卡生命周期状态机 + 状态转换测试场景集)
tags: [ppc, card, lifecycle, state-machine, test-cases]
related_services: [svc_ppc]
related_tables: [tbl_ppc_t_virtual_card]
related_logs: []
---

# PPC 卡生命周期状态转换测试场景集

## 触发 / 入口
基于 PPC 卡生命周期状态机推导的测试用例生成场景集,作为 AI 生成卡相关测试用例的事实基础。覆盖正向/反向状态转换、并发、配送子状态、多卡产品差异。配套接口与错误码见 [[reference_ppc_card_apis]],端到端流程见 [[flow_ppc_card_lifecycle]]。

## 关联关系
- **涉及服务**:[[svc_ppc]](= `related_services`);卡核心 [[svc_cards]] 相关。出向卡组织 YSE/Jaywan、解锁 PIN 走 APIPTR(待补对象)。
- **校验的表**:[[tbl_ppc_t_virtual_card]](= `related_tables`,status 字段流转)。
- **相关日志**:待补。

## 状态机定义

### 合法状态转换表
| from | to | 触发动作 | 前置条件 | 后置动作 |
| --- | --- | --- | --- | --- |
| (none) | A | 用户申请虚拟卡 | KYC=Tier2,已设支付密码,同会员同类型卡数 < 上限 | 创建 t_virtual_card 记录,调 YSE/Jaywan 申请 |
| A | U | 卡组织发卡成功通知 | YSE/Jaywan 返回成功 | 推送通知"卡片已就绪" |
| A | (申请失败) | 卡组织发卡失败/超时 | — | 释放申请名额 |
| U | N | 用户激活(含 PIN 设置) | ProxyNumber/OTP/KYC 核身正确 | 推送通知"卡片已激活" |
| N | L | 用户主动锁卡 / PIN 错误超限(YSE ResponseCode=75) | 卡余额可正可负 | 阻止后续授权交易 |
| L | N | 用户解锁 / Reset PIN(调 APIPTR) | 核身通过 | 恢复授权 |
| N / L | CI | 用户主动关卡 / 系统批量停用(dormant) | 卡余额=0;待结算账户已清空;余额同步完成 | 创建关卡订单(FeeFlag=N, Flag=C, Amount=0) |
| CI | C | 卡组织确认关卡 | 关卡订单支付成功/订单完成回调 | 推送通知"卡已关闭" |

### 非法转换(反向用例必出)
| 非法转换 | 风险 | 反向用例断言 |
| --- | --- | --- |
| C → 任意 | 已销卡仍可操作 = 资损 | 销卡后调激活/锁/解锁/查余额/授权 → 返回 `INVALID_CARD_STATUS` |
| A → N/L/CI/C | 跳过激活直达使用态 | 申请中调激活/锁/关卡 → 必拒 |
| U → L/CI | 未激活直接锁/关 | 未激活卡调锁卡 → 后端实际行为待确认,测试断言保持一致 |
| CI → N/L | 关卡中可被恢复 = 资金归属混乱 | 关卡中调激活/解锁 → 必拒 |
| 余额 ≠ 0 时关卡 | 资金未清退 | 构造非零余额发起关卡 → 返回 `NON_ZERO_BALANCE`(`DeactivateCardResultCode`) |

### 物理卡配送子状态(与虚拟卡状态正交)
基于 4.10.0 release Bug 推断:
| 状态 | 含义 | 关键转换触发 |
| --- | --- | --- |
| Preparing your physical card | 已下单制卡中 | 用户支付制卡费成功 |
| Out for delivery | 配送中 | Jeebly API status=Out for delivery |
| Delivered | 已送达 | Jeebly API status=Delivered |
| Cancelled | 用户取消 | 用户主动取消订单 |
| RTO Delivered | 退回原址 | Jeebly API status=RTO Delivered |
| Delivery cancelled | 配送失败 | Jeebly API failure |

**资损/UX 红线**:`Cancelled` / `RTO Delivered` 后必须等待 **7 天** 才能重新下物理卡(可配置,参考 WALLET-925)。

### PIN 状态
| PIN 状态 | 触发 | 解除条件 |
| --- | --- | --- |
| Not set | 卡刚激活 | 用户首次设 PIN |
| Set | 用户设过 PIN | — |
| Locked | 授权 ResponseCode=75(连续输错到上限) | 调 APIPTR 重置(Reset PIN) |

## 前置条件
- 会员 KYC=Tier2,已设置支付密码。
- 同一会员同类型卡数量 < 上限。
- 卡产品类型已知(MC=MULTI_CURRENCY / PR=PAY_ROLL);身份证件类型与卡产品匹配(MC 允许 EID/VIP_EID;PR 允许 EID/PASSPORT/VIP_EID)。
- 关卡前置:卡余额=0、待结算账户已清空、余额同步完成。
- 配送子状态测试依赖 Jeebly API 状态回调。

## 操作步骤(测试用例族)
**正向(合法转换)**:申请→A;发卡成功→U;激活→N;锁卡/ResponseCode=75→L;解锁/Reset PIN→N;关卡→CI;卡组织确认→C。
**反向(非法转换)**:C→任意(5 条,销卡后操作);A→使用态;U→L/CI;CI→N/L;非零余额关卡。
**并发**:同卡同时锁+解锁;关卡中(CI)再次发起关卡(幂等校验)。
**配送子状态**:6 状态 × 关键操作(重新下单、追踪、激活)≥18 条。
**多卡产品差异**:MC 走 dormant cleanup 批量停用;PR 跳过。

## DB 校验点
- t_virtual_card.status 在每次转换后等于目标 enum 值(A/U/N/L/CI/C)。
- 关卡订单字段:FeeFlag=N, Flag=C, Amount=0。
- 申请失败后申请名额计数已释放。
- 销卡后(C)任何写操作不改变 t_virtual_card 行。
- Cancelled / RTO Delivered 后 7 天内重新下物理卡 → 拒绝。

## 预期结果
- **正向**:每条合法转换成功,状态字段正确流转,触发对应后置动作(推送通知 / 调 YSE/Jaywan/APIPTR)。
- **反向**:C→任意返回 `INVALID_CARD_STATUS`;A/CI→激活/解锁/锁卡必拒;非零余额关卡返回 `NON_ZERO_BALANCE`。
- **并发**:重复关卡幂等,不产生多笔关卡订单;同时锁/解锁有明确串行结果。
- **配送红线**:Cancelled / RTO Delivered 后必须等 7 天才能重新下物理卡。
- **PIN**:授权 ResponseCode=75 触发 PIN Locked,需调 APIPTR Reset PIN 解除。
- **产品差异**:dormant cleanup 仅停用 MC 卡,PR 卡跳过。

## 用例规模估算
- 正向 ~9 条 + 反向(含销卡后操作 ≥5)+ 并发 2 条 + 配送 ≥18 条 + 多产品差异。
- 外部参考:`ppc-SD-Manually Deactivate Card`(真实 VirtualCardStatus / DeactivateCardResultCode enum)、`ppc-系统设计-1-卡管理`。
