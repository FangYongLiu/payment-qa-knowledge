---
id: scn_zand_fundout_test_cases
object_type: Scenario
domain: fund-out-transfer
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:AQ/2049867832
tags:
- zand
- fundout
- test-cases
- e2e
subdomain: zand
module: testing
sensitivity: normal
name: ZAND Fundout核心测试用例集
aliases: []
related_services: []
related_tables:
- tbl_mhtfundout_t_fundout_order
- tbl_mhtfundout_t_fundout_bankcard_order
- tbl_cmf_tt_inst_order
- tbl_cmf_tt_inst_order_result
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
覆盖ZAND渠道Fundout的10个核心测试用例，触发入口包括：
- Merchant Portal (uat-web-merchant.test2pay.com)：TC-001、TC-005、TC-006
- API测试框架 cgs-apitest：TC-002、TC-008、TC-009、TC-010
- BMOC Counter (uat-admin.corp.test2pay.com/counter/)：TC-003、TC-004
- Botim App：TC-007

## 前置条件
- 已连接公司VPN
- DBeaver / SQL Query Portal / Kibana 可用
- 测试账号可用：
  - 200000080798 (Test merchant, API SWIFT)
  - 200000086193 (TestABC, Portal 域内)
  - 200000079033 (0529ZXY01, Portal 国际)
- Mock VS HMAC Key (UAT)：`CoQnNYbgefTzpvhV1yr8L/Q7RX0m/JjsWMEFmQRFTj8=`
- Mock VS Target URL：`https://uat-fcw.test2pay.com/fcw/zand/notify`
- 测试IBAN：`AE170961002031010000003`

## 操作步骤

### TC-001 Domestic transfer via Merchant Portal (ZAND201) — P0 E2E
1. 登录 Merchant Portal，Partner=200000086193
2. Fiat -> Transfer -> Transfer to Bank
3. 输入 IBAN `AE170961002031010000003`，小额 AED，确认
4. 在 My Authorization 授权
5. 等待约15秒

### TC-002 International SWIFT transfer via API (ZAND203) — P0 API/E2E
```
cd cgs-apitest
python3 -m pytest testcases/payment/toB/test_placeTransferToBank_fangyong.py::TestPlaceTransferToBank::test_placeTransferToBankOrder_SWIFTUSD -s --env uat
```
等待真实 VS 或发送 Mock VS。

### TC-003 Settlement domestic (ZAND204) via BMOC — P1 E2E
1. BMOC -> Settlement Manage -> Settlement Detail -> Apply Settlement
2. Audit -> Audit List -> Approve
3. 验证渠道走 ZAND204（域内，约15秒）

### TC-004 Settlement international (ZAND207) via BMOC — P1 E2E
1. 同 TC-003 入口提交国际结算申请
2. 审核通过
3. 渠道走 ZAND207，需等 VS 回调

### TC-005 Merchant portal withdrawal domestic (ZAND210) — P1 E2E
Merchant Portal -> Fiat -> Withdrawal -> 选择本地 UAE 银行 -> 确认 -> 授权 (channel ZAND210)

### TC-006 Merchant portal withdrawal international (ZAND203) — P1 E2E
Partner 200000079033 -> Fiat -> Withdrawal -> 选择银行(USD) -> 确认 -> 授权

### TC-007 Personal withdrawal via App (ZAND201) — P1 E2E
Botim App -> Cards & Accounts -> Bank Accounts -> 选择 ZAND 账户 -> Withdraw funds -> 确认

### TC-008 Mock VS callback validation — P2 API
1. 从 DB 取 ChannelRefId (ZIT...) 和 CMF 订单号
2. 编辑 Zand.java mock tool，填入正确的 amount / channel_ref / instruction_id
3. 使用 HMAC Key (UAT) 与 Target URL
4. 编译并运行
5. 校验 DB 中 VS 行写入

### TC-009 SQ polling flow validation — P2 API
- 提交 ZAND203 订单，观察 SQ 轮询：
  - 前2分钟内开始
  - 间隔逐步增大
  - RETRY_TIMES > 35 时间隔为小时级
  - RETRY_TIMES = 54 时停止

### TC-010 Extension fields consistency (SP/SQ/VS) — P2 API
对比 SP / SQ / VS 三行 EXTENSION 字段，确认 CreationDateTime、ChannelRefId、channelTransTime 一致。

## DB 校验点

```sql
-- Fundout 订单
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

SP/SQ/VS 校验清单：
| 步骤 | 校验内容 |
|---|---|
| SP | INST_STATUS=I, INST_SEQ_NO=D.../ZIT..., EXTENSION 含 CreationDateTime+ChannelRefId+channelTransTime |
| SQ (仅国际) | INST_STATUS=I 或 S，ChannelRefId 相同，EXTENSION 与 SP 一致 |
| VS (域内) | INST_STATUS=S, MEMO=Credited To Beneficiary, Type=OUTGOING_DOMESTIC_TRANSACTION_STATUS |
| VS (国际) | INST_STATUS=S, MEMO=PROCESSED, Type=OUTGOING_INTERNATIONAL
