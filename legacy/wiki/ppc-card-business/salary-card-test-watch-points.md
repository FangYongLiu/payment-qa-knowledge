---
title: Salary Card Mono/Co-badge 测试关注点与回归矩阵
domain: ppc-card-business
kind: wiki_page
slug: salary-card-test-watch-points
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2167636024
tags: []
---

# Salary Card Mono/Co-badge 测试关注点与回归矩阵

本页汇总 Salary Card Mono / Co-badge 上线前必须覆盖的 15 个 Test Watch Points、测试数据/环境准备、与现有 Zephyr 用例的复用关系，以及新增用例的优先级建议。背景与业务定义见 [[salary-card-mono-cobadge-overview]]，PRD 评审上下文见 [[prd-review-salary-card-mono-cobadge-2026-05-13]]。

## 测试投入估算

基于 KB 用例生成模型，预估新增用例 **~100~120 条**（不含照抄 happy-path）：

- **资损红线触发**：~20 条 RL（多币种 8 + Auth-Clearing 4 + 状态机 3 + 对账 5）× 2~3 变体 ≈ **50~60 条**
- **易错模式触发**：12 个相关 EP × 平均 1.5 条 ≈ **18 条** 反向用例
- **PRD 特有场景**（BIN 路由 / Mono hard-fail / 双 Tokenization 等）：**~30 条**
- **现有 Zephyr 复用**：Mastercard 侧 70+ 条可复用，Jaywan 侧基本空白需新建

## 15 个 Test Watch Points

### 准入级（UAT 准入前必须完成）

| # | Watch point | 触发依据 | 现有用例复用 |
|---|---|---|---|
| **W1** | **BIN 路由错配检测**：构造 BIN 配错 product_code 的卡，验证授权拒绝并告警，不能误路由 | EP-019；Salary Card 是新产品 | 暂无 — 必须新增 |
| **W2** | **Mono 卡 hard-fail 国际交易**：Mono 卡发起非 AED / 跨境 acquirer 授权 → 必拒，错误码 & 用户文案对得上 PRD | PRD §3.3 + 卡组织规则差异 §3.2 | 暂无 — 必须新增 |
| **W3** | **Co-badge AED 走 Jaywan / FX 走 MC 路由正确性**：每个 currency × 每个 acquirer 组合各 1 条 | PRD §3.3 + EP-019 | 暂无 — 必须新增 |
| **W6** | **RL-026 对账文件解析**：Jaywan clearing / MC IPM 文件含 Intercharge Fee 时入对应 Profit Account；字段缺失时兜底 | RL-026 | 暂无 — 必须新增（Jaywan 文件格式新） |
| **W7** | **RL-009~RL-013 对账差错**：YSE 文件多于本地 auth / 少于 / 金额不一致 三档；Jaywan vs MC ledger 各跑 | RL-009~RL-013 | 暂无 — 必须新增 |
| **W8** | **RL-018~RL-020 状态机非法转换**：CLOSED 仍授权 / NON_ZERO_BALANCE 关卡 / CLOSING 中再关卡 | RL-018~020 + EP-005/EP-007 | 根 1 PAYM-T4538~T4565（Jaywan Card Management 53 条）部分覆盖；需扩到 co-badge |

### Cert 级（认证阶段必须完成）

| # | Watch point | 触发依据 | 现有用例复用 |
|---|---|---|---|
| **W4** | **RL-001~RL-008 多币种利润核算**（Co-badge 跨境时全套 P&L） | 二层资损红线 | PAYM-T9567/T9568/T9569（Multi-Currency Card Transaction Check / Configuration / Amount Check）部分覆盖换汇精度；co-badge 路径需补 |
| **W5** | **RL-014~RL-017 PA Completion / 余额不足 / No-auth Pre-auth completion** | 二层资损红线 | 根 1 PAYM-T5627~T5658（Transaction 接口测试）覆盖 MC 侧；Jaywan 侧 + Co-badge 路径需补 |
| **W12** | **3DS 双 ACS 路径**：Jaywan ECOM dual-message + 3DS / MC ECOM + 3DS 各一遍；3DS 失败兜底 | 卡组织规则差异 §3.5 | PAYM-T9295~T9314（3DS Auth）覆盖 MC；Jaywan 路径需补 |

### Soft launch / Canary 阶段可补

| # | Watch point | 触发依据 | 现有用例复用 |
|---|---|---|---|
| **W9** | **EP-001 弱网重复点击**：申请 / 激活 / 锁卡 / 关卡 / Reset PIN 五处都测，断言 DB 只 1 条记录 | EP-001 + BUG-6548/6554/8419 | Multi-Currency Card 主流程多条覆盖；Salary Card co-badge UI 路径需补 |
| **W10** | **EP-008~EP-010 异步消息时序**：Clearing 先于 Auth、message 重投、NARADA 反向回环 | RL-028~RL-030 + EP-008/009/010 | 暂无 — 必须新增 |
| **W11** | **双 Tokenization 单边失败**：MC token OK + Jaywan token 失败 / 反之；PAN suspended 时两 DPAN 联动 | EP-020/EP-022 + PRD §4.1 | 暂无 — 必须新增 |
| **W13** | **Jaywan 历史 Bug 回归**：BUG-7425（绑定确认按钮错误）、BUG-6936（地址回填缺失）、BUG-7689（交易历史）、BUG-7781（申请后状态检查） | 四层历史 Bug 库（PPC-Jaywan-* 标签 23 条） | 现有用例覆盖不全，建议这 4 条 P1/P2 bug 全部建为 Salary Card 回归 |
| **W14** | **EP-018 配置漂移**：UAT/SIM/PROD Jaywan 沙箱配置一致性（BIN、限额、费率、MCC、错误码） | EP-018 + 五层环境差异表 | 暂无 — 必须新增配置 diff 检查脚本 |
| **W15** | **跨境费 3.5% vs KB 2.00% 实际取值**（PM 拍板后） | 限额体系冲突项 | 暂无 — 必须新增 |

## 测试数据 / 环境准备

| # | 准备项 | KB ref |
|---|---|---|
| **D1** | **新测试卡 BIN**：Jaywan Mono BIN + Co-badge MC Gold BIN 各分配 Sandbox 测试卡；同物理 PAN 两 DPAN 测试卡 | 五层 测试卡资源 `2133328021` — 上线后必须回填 |
| **D2** | **金额边界值集**：ATM 单笔 2,999.99 / 3,000.00 / 3,000.01；POS 9,999.99 / 10,000.00 / 10,000.01；含 BHD/KWD 三位精度（EP-011） | 五层 金额边界值集 `2134966340` + EP-011/EP-012 |
| **D3** | **MCC 测试集**：白名单（5411）+ 黑名单（7995
