---
id: scn_cko_subscription_test_cases
object_type: Scenario
domain: channel-integration
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki_attachment
source_ref: wiki_attachment:af0d55d4-10d6-454b-b0a9-8ff7e104cd04
tags:
- CKO
- 订阅支付
- 测试用例
subdomain: cko
module: null
sensitivity: normal
name: CKO订阅支付测试卡用例
aliases: []
related_services: []
related_tables: []
related_scenarios:
- scn_cko_standalone_card_binding
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
CKO订阅支付测试场景，按收银台形态与业务类别拆分为多个 Sheet：
- Old Cashier（老收银台）
- New Cashier（新收银台）
- Standalone Binding（独立绑卡）
- Special Business（特殊业务）
- Regression（回归测试）

## 前置条件
各 Sheet 共有 Prerequisites 模块（Module description: Prerequisites），用于声明该类用例执行前的环境与数据准备要求。

## 操作步骤
按 Sheet 分类组织用例：

### Old Cashier（老收银台）
- Category：用例分类
- Normal flow：正常流
- Exception flow：异常流
- Payment auth + risk rules：支付鉴权 + 风控规则

### New Cashier（新收银台）
- Category：用例分类
- Standard cashier：标准收银台
- Exception flow：异常流

### Standalone Binding（独立绑卡）
- Category — Case No.：用例分类与编号，Card contract info linked to Card_id 字段记录绑卡合约信息
- Standalone binding 用例编号 1 ~ 7（每条用例对应一个 Card_id 关联的绑卡合约信息）

### Special Business（特殊业务）
- Category：用例分类
- Special business (normal)：特殊业务（正常流）

### Regression（回归测试）
- Category：用例分类
- Regression：回归用例

## DB 校验点
独立绑卡用例需校验 Card contract info 与 Card_id 的关联信息（Case No. 1 ~ 7）。

## 预期结果
- 老收银台：正常流通过、异常流被拦截、支付鉴权与风控规则按预期触发
- 新收银台：标准收银台正常流通过、异常流被拦截
- 独立绑卡：7 条用例对应的 Card 合约与 Card_id 正确建立关联
- 特殊业务：正常流通过
- 回归：历史用例全部通过
