---
title: ZAND Fundout测试方法指南
domain: fund-out-transfer
kind: wiki_page
slug: zand-fundout-test-guide
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:7f334321-3b49-4c87-b6d9-8949925a962a
tags: []
---

# ZAND Fundout测试方法指南

本页汇总 ZAND Fundout 在 UAT 环境下的测试方法：环境准备、测试账号、五类典型场景的执行步骤、Mock VS 回调工具用法，以及 SP/SQ/VS 三阶段的 SQL 校验清单。业务背景与系统链路见 [[zand-fundout-overview]] 与 [[zand-fundout-system-architecture]]；端到端流程见 [[flow_zand_fundout]]；用例集见 [[scn_zand_fundout_test_cases]]。

## 测试环境

| 工具 | 地址 / 位置 | 用途 |
|---|---|---|
| VPN | 公司 VPN | 访问所有内部系统的前提 |
| Merchant Portal | uat-web-merchant.test2pay.com | 发起转账、提现 |
| BMOC Counter | uat-admin.corp.test2pay.com/counter/ | 结算管理与审核 |
| DBeaver | dbeaver.io | 只读 SQL 查询 |
| SQL Query Portal | sqlquery-uat.test2pay.com | 写库操作 |
| Kibana | 内部 URL | 日志追踪 |
| 代码仓库 | cgs-apitest (Git) | API 测试框架与 Mock VS 工具 |

DBeaver 连接：Host `mysql-rds-uat-pby-aen-001.mysql.database.azure.com`，Port `3306`，Username `reader` / `cmfuser`（只读）。

## 测试账号

| Partner ID | 名称 | 类型 | 用途 |
|---|---|---|---|
| 200000080798 | Test merchant | Merchant (API) | API 方式 SWIFT 转账 |
| 200000086193 | TestABC | Merchant (Portal) | 商户后台境内转账 |
| 200000079033 | 0529ZXY01 | Merchant (Portal) | 商户后台国际提现 |

## 场景 A：境内转账 ZAND201（Merchant Portal）

- 登录 Merchant Portal，Partner: `200000086193`
- 路径：Fiat → Transfer → Transfer to Bank
- 输入 IBAN `AE170961002031010000003`，小额 AED，确认提交
- 在 My Authorization 中授权
- 等待约 15 秒，库内校验：
  - `t_fundout_order.status = SUCCESS`
  - CMF 走 `ZAND201` 渠道
  - `tt_inst_order_result` 中存在 SP + VS 两条记录

## 场景 B：国际 SWIFT 转账 ZAND203（API）

```bash
cd cgs-apitest
python3 -m pytest testcases/payment/toB/test_placeTransferToBank_fangyong.py::TestPlaceTransferToBank::test_placeTransferToBankOrder_SWIFTUSD -s --env uat
```

随后等待真实 VS 回调，或使用 Mock VS 工具触发（见下文）。

## 场景 C：结算 ZAND204 + ZAND207（BMOC）

- BMOC → Settlement Manage → Settlement Detail → Apply Settlement
- Audit → Audit List → Approve
- 验证：
  - ZAND204（境内，快速）
  - ZAND207（国际，依赖 VS 回调）

## 场景 D：商户后台提现

- 国际（USD）：Partner `200000079033` → Fiat → Withdrawal → 选择银行 → 确认 → 授权
- 境内（AED）：同上流程，选择 UAE 本地银行（渠道 `ZAND210`）

## 场景 E：个人提现 ZAND201（App）

- Botim App → Cards & Accounts → Bank Accounts → 选择 ZAND 账户 → Withdraw funds → 确认

## Mock VS 回调工具

国际订单需通过 VS 完成最终状态更新，UAT 可使用 Mock VS 工具模拟回调，详见 [[auto_zand_mock_vs_tool]]：

1. 从 DB 取得 ChannelRefId（`ZIT...`）与 CMF 订单号
2. 编辑 `Zand.java`，填入正确的 amount、channel_ref、instruction_id
3. 使用 UAT HMAC Key：`CoQnNYbgefTzpvhV1yr8L/Q7RX0m/JjsWMEFmQRFTj8=`
4. 目标 URL：`https://uat-fcw.test2pay.com/fcw/zand/notify`
5. 编译运行后，验证 DB 中新增 VS 行

## 关键校验 SQL

涉及表见 [[tbl_mhtfundout_t_fundout_order]]、[[tbl_mhtfundout_t_fundout_bankcard_order]]、[[tbl_cmf_tt_inst_order]]、[[tbl_cmf_tt_inst_order_result]]、[[tbl_router_t_channel_result_code]]。

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

## SP / SQ / VS 校验清单

| 阶段 | 关键校验点 |
|---|---|
| SP | `INST_STATUS=I`；`INST_SEQ_NO` 为 `D...`（境内）或 `ZIT...`（国际）；`EXTENSION` 含 `CreationDateTime` + `ChannelRefId` + `channelTransTime` |
| SQ（仅国际） | `INST_STATUS=I` 或 `S`；ChannelRefId 与 SP 一致；EXTENSION 与 SP 一致 |
| VS（境内） | `INST_STATUS=S`；`MEMO=Credited To Beneficiary`；Type=`OUTGOING_DOMESTIC_TRANSACTION_STATUS` |
| V
