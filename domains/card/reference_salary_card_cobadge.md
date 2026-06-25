---
id: reference_salary_card_cobadge
object_type: reference
name: Salary Card Mono-badge & Co-badge 产品/路由/测试关注点
aliases: [Salary Card Mono-badge, Salary Card Co-badge, SALCOB, SALMOB, salary card test watch points]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2167636024 (Salary Card Mono/Co-badge 总览 + PRD review 2026-05-13 + 测试关注点)
tags: [salary-card, co-badge, mono-badge, jaywan, mastercard, bin-routing, tokenization, 3ds]
related_services: [svc_ppc]
---

# Salary Card Mono-badge & Co-badge 产品/路由/测试关注点

> Salary Card 引入两个新 program:**Jaywan Mono-badge**(仅 AED 国内,国际硬拒)与 **MC × Jaywan Co-badge**(同一物理 PAN,AED 走 Jaywan / FX 跨境走 Mastercard MIP),满足 **CBUAE 2026-03-31 AEP Mandate**。目标 EOY 150K cards、Mono:Co-badge ≈ 80:20、节约 ~400K AED。卡生命周期见 [[scn_card_lifecycle_transitions]],Jaywan 集成见 [[reference_jaywan_mbank_integration]] 与 [[flow_jaywan_prepaid_card]]。

## 产品定义与边界
- **Mono-badge**:单一卡组织=Jaywan;仅支持 AED 国内交易,国际硬拒(判定字段——currency!=AED / acquiring country / BIN——PRD 未明确)。
- **Co-badge**:Mastercard Prepaid Gold BIN + Jaywan onboard;同一物理 PAN,AED 走 Jaywan、FX/跨境走 MC MIP。
- 发卡链路:BPS(业务系统)→ PPC(托管)→ YSE(卡管理)→ EDC(印卡)→ Botim App(用户端);企业批量发卡走 Corporate Management。

## 产品编码与 BIN 路由
- 新 product code:**SALCOB**(Co-badge)/ **SALMOB**(Mono);新 plastic code **STDPLS***。
- `t_card_bin` 表区分双 scheme,按 `BIN + product_code` 路由;Card lifecycle CMS 调 YSE API 时按 BIN+product_code 决策,存 scheme 偏好。
- Auth Router:`SAL_JAY_MONO`(AED→Jaywan);`SAL_CO_BADGE`(AED→Jaywan;FX→MC MIP)。
- ⚠️ PRD 未给出灰度/canary、误配检测、rollback 策略 —— **BIN 路由错配(EP-019)是最大风险点**。

## 交易链路
- 域内(UAE)五段式:`Customer → Acquirer → UAESWITCH → Jaywan → Botim/YSE → PPC`。Jaywan ECOM=dual-message;POS/ATM=single-message;YSE PBAUTH 用 proxy_no 识别 scheme。
- 国际跨境:Co-badge FX 归入 Mastercard 既有 MIP 框架;Mono 卡 hard-fail 国际交易。

## 清算 / 对账 / Ledger
- 新 ledger 三类账户:**jaywan pre-settlement / Jaywan Pending / MC Pending**(⚠️ 与 KB 限额体系现行命名 Customer Basic/Pending/Merchant Basic/Profit/Shortfall 不一致,需明确映射)。
- Jaywan clearing 文件格式与 MC IPM 不同,需单独 ingest;每日三方对账(scheme vs processor vs ledger)。
- ⚠️ 未覆盖:对账文件解析失败兜底、双 ledger Shortfall 归属、字段缺失/金额漂移。

## Tokenization / 3DS
- 双 token service provider:同一物理 PAN 在设备钱包可能产生 2 个 DPAN(MC 一个 / Jaywan 一个);存 scheme、token_reference、lifecycle 状态。
- ⚠️ Open:PAN suspended/closed 时两 DPAN 是否联动 revoke、单边 token 创建失败的卡状态、scheme 单边 lifecycle 通知如何同步另一 scheme。
- 3DS 双 ACS(Jaywan 与 MC 各一套),配置 per product_code;⚠️ Open:双 scheme challenge/frictionless 决策是否一致。

## 费率与限额
| 项目 | Mono (Jaywan) | Co-badge (MC × Jaywan) |
| --- | --- | --- |
| 发卡费 | 0~25 AED | — |
| 补卡费 | 26.25 AED | — |
| ATM 取现 | 2.05 AED | — |
| 余额查询 | 1.05 AED | — |
| 跨境/跨币种费 | n/a(硬拒国际) | **3.5%**(与 KB 现行 2.00% 冲突,待 PM 拍板) |
| ATM 单笔 | 3,000 AED | 3,000 AED |
| POS / Ecom 单笔 | 10,000 AED | 10,000 AED |
| 日 / 月限额 | "as per wallet specifications"(未明确) | 同左 |

> ⚠️ 多币种限额是否按 AED 等值合并、跨境费率最终值,均为 Open Question。

## 认证与环境
- 三环境 dev→UAT→pre-prod→prod;Jaywan UAT rails 经 YSE。
- Mastercard 必过认证:CAA / CPV / IHC / Ecom / Tokenization(各项 timeline/owner 待补,对齐 CBUAE 2026-03-31)。

## 测试关注点(15 个 Test Watch Points)
预估新增用例 ~100~120 条(资损红线 ~50~60 + 易错模式 ~18 + PRD 特有 ~30;Mastercard 侧 Zephyr 70+ 可复用,Jaywan 侧基本空白)。

### 准入级(UAT 准入前必须完成)
- **W1 BIN 路由错配检测**:BIN 配错 product_code → 授权拒绝并告警,不误路由(EP-019)。新增。
- **W2 Mono 卡 hard-fail 国际交易**:非 AED/跨境 acquirer 授权必拒,错误码 & 用户文案对得上 PRD。新增。
- **W3 Co-badge 路由正确性**:AED 走 Jaywan / FX 走 MC,每个 currency × acquirer 组合各 1 条。新增。
- **W6 RL-026 对账文件解析**:Jaywan clearing / MC IPM 含 Interchange Fee 入对应 Profit Account;字段缺失兜底。新增(Jaywan 格式新)。
- **W7 RL-009~013 对账差错**:YSE 文件多于/少于本地 auth/金额不一致三档;Jaywan vs MC ledger 各跑。新增。
- **W8 RL-018~020 状态机非法转换**:CLOSED 仍授权 / NON_ZERO_BALANCE 关卡 / CLOSING 中再关卡(参见 [[scn_card_lifecycle_transitions]])。部分复用,需扩到 co-badge。

### Cert 级(认证阶段)
- **W4 RL-001~008 多币种利润核算**(Co-badge 跨境全套 P&L)。
- **W5 RL-014~017 PA Completion / 余额不足 / No-auth Pre-auth completion**(MC 侧已覆盖,Jaywan+Co-badge 需补)。
- **W12 3DS 双 ACS 路径**:Jaywan ECOM dual-message+3DS / MC ECOM+3DS 各一遍;3DS 失败兜底。

### Soft launch / Canary 阶段
- **W9 EP-001 弱网重复点击**:申请/激活/锁卡/关卡/Reset PIN 五处,断言 DB 只 1 条(BUG-6548/6554/8419)。
- **W10 EP-008~010 异步消息时序**:Clearing 先于 Auth、message 重投、NARADA 反向回环。新增。
- **W11 双 Tokenization 单边失败**:MC token OK + Jaywan 失败/反之;PAN suspended 时两 DPAN 联动(EP-020/022)。新增。
- **W13 Jaywan 历史 Bug 回归**:BUG-7425(绑定确认按钮)、BUG-6936(地址回填)、BUG-7689(交易历史)、BUG-7781(申请后状态检查)。
- **W14 EP-018 配置漂移**:UAT/SIM/PROD Jaywan 沙箱配置一致性(BIN/限额/费率/MCC/错误码)。新增 diff 脚本。
- **W15 跨境费 3.5% vs KB 2.00%**(PM 拍板后)。

## 测试数据 / 环境准备
- **D1 新测试卡 BIN**:Jaywan Mono BIN + Co-badge MC Gold BIN 各分配 Sandbox 测试卡;同物理 PAN 两 DPAN 测试卡。
- **D2 金额边界值集**:ATM 2,999.99 / 3,000.00 / 3,000.01;POS 9,999.99 / 10,000.00 / 10,000.01;含 BHD/KWD 三位精度(EP-011)。
- **D3 MCC 测试集**:白名单(5411)+ 黑名单(7995 等)。MCC 测试集字段:MCC 编码(4 位)、业务名、分类(白/黑/高风险/普通)、适用卡产品、限额特殊配置、风控规则、合规要求、Sandbox 是否支持;覆盖白/黑名单 + 高风险(博彩/加密货币/成人)+ 普通超市/餐饮/加油/ATM/跨境,含 UAE 监管禁止的 MCC。

## PRD review 结论(2026-05-13)
- Verdict:**Needs Revision**。21 标准章节只覆盖 ~7;无 FR 编号、无 Edge Cases/Risks/Rollout/Testing Strategy 实质内容;编号体系冲突(两个 `## 3)`)。
- Critical:章节编号冲突;无 FR-NN+AC;缺 Risks/Edge Cases/Rollout/Migration/Timeline(CBUAE 2026-03-31 硬截止);EP-019 BIN 路由配置错误未对应(缺灰度/检测/回滚);资损红线 RL-001~008/RL-014~017/RL-026 未覆盖;Mono 卡国际硬拒实现细节缺(判定字段/错误码/用户提示/是否记账)。

## Glossary(PRD 中出现但未定义,待补)
CAA / CPV / IHC / IPM / MIP / UAESWITCH / proxy_no / NARADA / SVF / BPS / SALCOB / SALMOB / STDPLS*。
