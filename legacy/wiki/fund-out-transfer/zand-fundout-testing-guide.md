---
title: ZAND Fundout测试指南
domain: fund-out-transfer
kind: wiki_page
slug: zand-fundout-testing-guide
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2049867832
tags: []
---

# ZAND Fundout测试指南

本页面整理 ZAND Fundout 在 UAT 环境下的测试入口、测试账号、各场景执行步骤、Mock VS 工具用法以及关键校验 SQL，覆盖商户后台、BMOC、API 与 App 五类入口。相关业务背景见 [[zand-fundout-overview]]，系统调用细节见 [[zand-fundout-system-architecture]]，问题定位见 [[zand-fundout-troubleshooting]]。

## 测试环境与工具

| 工具 | 地址 / 位置 | 用途 |
|---|---|---|
| VPN | 公司 VPN 客户端 | 访问内网系统的前置条件 |
| Merchant Portal | uat-web-merchant.test2pay.com | 商户后台发起 Transfer / Withdrawal |
| BMOC Counter | uat-admin.corp.test2pay.com/counter/ | 结算管理与审核 |
| DBeaver | dbeaver.io | 数据库只读查询 |
| SQL Query Portal | sqlquery-uat.test2pay.com | 数据库写操作 |
| Kibana | 内部 Kibana | 日志追踪 |
| 代码仓库 | cgs-apitest (Git) | API 测试框架 + Mock VS 工具 |

DBeaver 连接信息：
- Host：`mysql-rds-uat-pby-aen-001.mysql.database.azure.com`
- Port：3306
- 只读账号：`reader` / `cmfuser`

## 测试账号

| Partner ID | 名称 | 类型 | 用途 |
|---|---|---|---|
| 200000080798 | Test merchant | Merchant (API) | API 方式 SWIFT 国际转账 |
| 200000086193 | TestABC | Merchant (Portal) | 商户后台境内转账 |
| 200000079033 | 0529ZXY01 | Merchant (Portal) | 商户后台国际提现 |

## 测试方法（按场景）

完整用例集见 [[scn_zand_fundout_test_cases]]，端到端流程见 [[flow_zand_fundout]]。

### A. 境内转账 ZAND201（商户后台）

1. 登录 Merchant Portal，Partner `200000086193`
2. Fiat → Transfer → Transfer to Bank
3. 输入 IBAN `AE170961002031010000003`，小额 AED，确认
4. 在 My Authorization 中授权
5. 等待约 15s，校验 DB：fundout `status=SUCCESS`，CMF 渠道 `ZAND201`，存在 SP + VS 记录

### B. 国际 SWIFT 转账 ZAND203（API）

```
cd cgs-apitest
python3 -m pytest testcases/payment/toB/test_placeTransferToBank_fangyong.py::TestPlaceTransferToBank::test_placeTransferToBankOrder_SWIFTUSD -s --env uat
```

执行后等待真实 VS 回调，或使用 Mock VS 工具补发。

### C. 结算 ZAND204 + ZAND207（BMOC）

1. BMOC → Settlement Manage → Settlement Detail → Apply Settlement
2. Audit → Audit List → Approve
3. 校验 ZAND204（境内，快速）与 ZAND207（国际，需 VS）

### D. 商户后台 Withdrawal

- 国际 USD：Partner `200000079033` → Fiat → Withdrawal → 选择银行 → 确认 → 授权
- 境内 AED：同流程，选择 UAE 本地银行（渠道 ZAND210）

### E. 个人 App 提现 ZAND201

Botim App → Cards & Accounts → Bank Accounts → 选择 ZAND 账户 → Withdraw funds → 确认

## Mock VS 回调工具

国际订单需要 VS 才能完结时使用，详见 [[auto_zand_mock_vs_tool]]。

操作步骤：
1. 从 DB 取到 `ChannelRefId`（`ZIT...`）和 CMF 订单号
2. 编辑 `Zand.java` mock 工具，填入正确的 amount、channel_ref、instruction_id
3. UAT HMAC Key：`CoQnNYbgefTzpvhV1yr8L/Q7RX0m/JjsWMEFmQRFTj8=`
4. 目标 URL：`https://uat-fcw.test2pay.com/fcw/zand/notify`
5. 编译并运行，校验 DB 中 VS 记录已写入

## 关键校验 SQL

订单主表见 [[tbl_mhtfundout_t_fundout_order]]，CMF 渠道单见 [[tbl_cmf_tt_inst_order]]，SP/SQ/VS 结果见 [[tbl_cmf_tt_inst_order_result]]。

```sql
-- Fundout 订单状态
SELECT global_id, status, product_code, created_time, unity_result_code
FROM mhtfundout.t_fundout_order
WHERE partner_id = '<partner_id>' ORDER BY global_id DESC LIMIT 5;

-- CMF 渠道订单
SELECT INST_ORDER_NO, FUND_CHANNEL_CODE, STATUS, CURRENCY, AMOUNT, GMT_CREATE
FROM cmf.tt_inst_order
WHERE FUND_CHANNEL_CODE = '<channel>' ORDER BY GMT_CREATE DESC LIMIT 5;

-- SP/SQ/VS 结果
SELECT INST_ORDER_NO, API_TYPE, INST_STATUS, MEMO, INST_SEQ_NO, EXTENSION, GMT_CREATE
FROM cmf.tt_inst_order_result
WHERE INST_ORDER_NO = '<order>' ORDER BY GMT_CREATE ASC;

-- 商户余额
SELECT BALANCE, CURRENCY FROM dpm.t_dpm_outer_account_subset s
JOIN dpm.t_dpm_outer_account a ON a.ACCOUNT_NO = s.ACCOUNT_NO
WHERE a.MEMBER_ID = '<partner_id>' AND a.ACCOUNT_TYPE = 1
  AND s.BALANCE_TYPE = 1 AND s.fund_type = 1 AND s.CURRENCY = 'AED';
```

## SP/SQ/VS 校验清单

| 步骤 | 校验点 |
|---|---|
| SP | `INST_STATUS=I`，`INST_SEQ_NO=D.../ZIT...`，EXTENSION 含 `CreationDateTime` + `ChannelRefId` + `channelTransTime` |
| SQ（仅国际） | `INST_STATUS=I` 或 `S`，ChannelRefId 与 SP 一致，EXTENSION 与 SP 一致 |
| VS（境内） | `INST_STATUS=S`，`MEMO=Credited To Beneficiary`，Type=`OUTGOING_DOMESTIC_TRANSACTION_STATUS` |
| VS（国际） | `INST_STATUS=S`，`MEMO=PROCESSED`，Type=`OUTGOING_INTERNATIONAL_
