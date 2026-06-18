---
title: 商户收单测试方法论总览
domain: merchant-acquisition-testing
kind: wiki_page
slug: merchant-acquisition-test-methodology-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2125922317
tags: []
---

# 商户收单测试方法论总览

本页定义商户收单测试的通用方法论，是所有场景手册（§5.x）依赖的"骨架"。先读懂本页，再去看具体场景。

## 核心理念

商户收单测试**不是只测商户接口**，而是要验证整条链路：

- 支付中台各服务的调用链
- 数据库落库
- 资金流（Fund Flow）
- 异步通知
- 对账文件

> 一笔成功的接口响应只是测试的**起点**，不是终点。只测前几段不测后几段，才会有"商户报已付款但订单未支付"、"对账不平"、"清算流水缺失"这类问题逃逸到生产。

## 方法论的四块拼图

本页方法论由以下四块组成，对应独立子页：

| 模块 | 作用 | 子页 |
|---|---|---|
| 测试环境与工具 | 域名、SGS、API Key、MySQL、测试账号、MID | [[merchant-acquisition-test-environment-tools]] |
| 五段式 E2E 验证骨架 | 所有场景都按 5 段验证，缺一不可 | [[merchant-acquisition-e2e-five-stage-verification]] |
| 标准用例骨架 A/B/C/D/E | 每个场景至少要覆盖 5 类用例 | [[merchant-acquisition-test-case-skeleton-abcde]] |
| 测试数据准备规范 | merchantOrderNo 命名 / 金额选择 / 卡号 / 回调 | [[merchant-acquisition-test-data-preparation]] |

## 五段式 E2E 验证骨架（核心方法论）

这是本方法论最重要的一节。所有场景手册的测试用例都按这 5 段来验证：

1. **接口响应**（API Response）—— HTTP 状态码、`applyStatus`、`code`、业务订单号、状态枚举
2. **服务调用链**（Service Log）—— 整条链路上每个服务都有日志、关键参数符合预期、无异常重试
3. **数据库落库**（DB Persistence）—— 每个相关表都增加/更新预期数量记录、状态/金额/关联字段正确
4. **Fund Flow**（资金流）—— 该不该产生入账流水、借贷平衡（Total Dr = Total Cr）、账户方向正确
5. **通知 & 对账**（Notify & Statement）—— `notifyUrl` 异步通知触发、商户回 `{"response":"SUCCESS"}` 后停止重试、T+1 对账单 CSV 包含本笔

详见 [[merchant-acquisition-e2e-five-stage-verification]]。

## 标准用例骨架（A/B/C/D/E）

每个场景至少覆盖 5 类用例：

- **A 组**：正向流程（Happy Path）
- **B 组**：异常流程（Negative Path）
- **C 组**：数据一致性（Consistency）
- **D 组**：边界与并发（Boundary & Concurrency）
- **E 组**：权限与安全（Auth & Security）

详见 [[merchant-acquisition-test-case-skeleton-abcde]]。

## 与场景手册（§5.x）的关系

- **本页是通用方法论**，不绑定具体业务场景
- 所有场景手册（PAYPAGE / DIRECTPAY / PREAUTH / Capture / Refund 等）都**按本页定义的 5 段验证骨架编写**
- 场景手册需明确给出"该场景下应增加的具体表+条数"清单，跑用例时按表打 ✓
- 错误码、curl 模板、每笔交易检查清单作为通用工具页存在

## 配套通用资料

- [[merchant-acquisition-error-code-cheatsheet]]：错误码速查（全局码 / 订单状态冲突 / 退款撤销 / 卡片产品 / 风控 / Capture-Void-PreAuth 专属 msg）
- [[merchant-acquisition-notify-statement-spec]]：异步通知重试时间表 + 对账单 ZIP/CSV 结构
- [[merchant-acquisition-curl-postman-templates]]：通用 Header、Create Order、Refund、Get Balance、对账单下载骨架
- [[merchant-acquisition-per-transaction-checklist]]：每跑一笔交易必走的核对清单（可打印贴任务卡片）

## 阅读路径建议

1. 先读 [[merchant-acquisition-test-environment-tools]] 把环境和账号搞通
2. 读 [[merchant-acquisition-e2e-five-stage-verification]] 理解 5 段验证骨架（**最重要**）
3. 读 [[merchant-acquisition-test-case-skeleton-abcde]] 和 [[merchant-acquisition-test-data-preparation]] 知道用例要覆盖哪些维度、数据怎么造
4. 跑用例时随手翻 [[merchant-acquisition-error-code-cheatsheet]] 和 [[merchant-acquisition-per-transaction-checklist]]
5. 进入具体场景手册：§5.1 PAYPAGE / §5.8 DIRECTPAY / §5.9 PREAUTH
