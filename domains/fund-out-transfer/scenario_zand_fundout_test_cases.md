---
id: scn_zand_fundout_test_cases
object_type: Scenario
domain: fund-out-transfer
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:7f334321-3b49-4c87-b6d9-8949925a962a
tags:
- zand
- fundout
- test-cases
subdomain: null
module: null
sensitivity: normal
name: ZAND Fundout核心测试用例集
aliases: []
related_services: []
related_tables:
- tbl_mhtfundout_t_fundout_order
- tbl_mhtfundout_t_fundout_bankcard_order
- tbl_cmf_tt_inst_order
- tbl_cmf_tt_inst_order_result
- tbl_router_t_channel_result_code
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
覆盖 ZAND Fundout 业务的 10 条核心测试用例(TC-001 ~ TC-010)，触发入口分布于：
- Merchant Portal：uat-web-merchant.test2pay.com (TC-001, TC-005, TC-006)
- API 测试框架 cgs-apitest (TC-002, TC-008, TC-009, TC-010)
- BMOC Counter System：uat-admin.corp.test2pay.com/counter/ (TC-003, TC-004)
- Botim App：Cards & Accounts -> Bank Accounts (TC-007)

## 前置条件
- VPN 已连接，可访问 UAT 内部系统
- DBeaver / SQL Query Portal 可用，用于查询 mhtfundout / cmf / dpm 等库
- 测试账号：
  - 200000086193 (TestABC) — 商户门户境内
  - 200000079033 (0529ZXY01) — 商户门户国际
  - 200000080798 — API SWIFT
- 国际单测试需 Mock VS 工具 Zand.java，HMAC key (UAT)：CoQnNYbgefTzpvhV1yr8L/Q7RX0m/JjsWMEFmQRFTj8=，回调 URL：https://uat-fcw.test2pay.com/fcw/zand/notify
- 商户门户转账需 My Authorization 授权；结算流程需 BMOC 审核审批

## 操作步骤
### TC-001 Domestic transfer via Merchant Portal (ZAND201, P0)
1. 登录 Merchant Portal (Partner: 200000086193)
2. Fiat -> Transfer -> Transfer to Bank
3. IBAN：AE170961002031010000003，输入小额 AED，确认
4. My Authorization 授权
5. 等待 ~15s 校验 DB

### TC-002 International SWIFT transfer via API (ZAND203, P0)
1. cd cgs-apitest
2. 执行：python3 -m pytest testcases/payment/toB/test_placeTransferToBank_fangyong.py::TestPlaceTransferToBank::test_placeTransferToBankOrder_SWIFTUSD -s --env uat
3. 等待真实 VS 或发送 Mock VS

### TC-003 Settlement domestic (ZAND204, P1)
1. BMOC -> Settlement Manage -> Settlement Detail -> Apply Settlement
2. Audit -> Audit List -> Approve
3. 校验 ZAND204 通道境内结算

### TC-004 Settlement international (ZAND207, P1)
1. 同 TC-003 流程，触发国际结算
2. 等待 VS 回调或发送 Mock VS
3. 校验 ZAND207 通道

### TC-005 Merchant portal withdrawal domestic (ZAND210, P1)
1. 商户门户 -> Fiat -> Withdrawal
2. 选择本地 UAE 银行 -> 确认 -> 授权
3. 校验路由至 ZAND210

### TC-006 Merchant portal withdrawal international (ZAND203, P1)
1. Partner 200000079033 -> Fiat -> Withdrawal
2. 选择银行 -> 确认 -> 授权
3. 校验 USD 国际提现走 ZAND203

### TC-007 Personal withdrawal via App (ZAND201, P1)
1. Botim App -> Cards & Accounts -> Bank Accounts
2. 选择 ZAND 账户 -> Withdraw funds -> 确认

### TC-008 Mock VS callback validation (P2)
1. 从 DB 取 ChannelRefId(ZIT...) 与 CMF order
2. 编辑 Zand.java：amount、channel_ref、instruction_id
3. 使用 UAT HMAC key 编译运行，回调至 fcw/zand/notify
4. 验证 DB 中 VS 行写入

### TC-009 SQ polling flow validation (P2)
1. 提交国际单后观察 SQ 轮询：SP 后前 ~2 分钟开始，间隔逐渐增大
2. RETRY_TIMES > 35 间隔变为小时级
3. RETRY_TIMES = 54 停止轮询

### TC-010 Extension fields consistency SP/SQ/VS (P2)
1. 取一条国际单订单
2. 查询 cmf.tt_inst_order_result 中 SP/SQ/VS 三行 EXTENSION 字段
3. 校验 CreationDateTime / ChannelRefId / channelTransTime 全程一致

## DB 校验点
- mhtfundout.t_fundout_order：status=SUCCESS，product_code 正确(220401/220402/230602)，unity_result_code 非 cmf.route.fail
- cmf.tt_inst_order：FUND_CHANNEL_CODE = ZAND201/203/204/207/210，STATUS=S，AMOUNT/CURRENCY 正确，RETRY_TIMES 行为符合预期
- cmf.tt_inst_order_result：
  - SP 行：INST_STATUS=I，INST_SEQ_NO 为 D...(境内) 或 ZIT...(国际)，EXTENSION 含 CreationDateTime + ChannelRefId + channelTransTime
  - SQ 行(仅国际)：INST_STATUS=I 或 S，ChannelRefId 与 SP 一致
  - VS 行(境内)：INST_STATUS=S，MEMO=Credited To Beneficiary，Type=OUTGOING_DOMESTIC_TRANSACTION_STATUS
  - VS 行(国际)：INST_STATUS=S，MEMO=PROCESSED，Type=OUTGOING_INTERNATIONAL_TRANSACTION_STATUS
- dpm.t_dpm_outer_account_subset：BALANCE 正确扣减(含手续费，例如国际 SWIFT 157.50 AED)
- router.t_channel_result_code：PROCESSED 映射 result_status=S

## 预期结果
- TC-001：~12 秒内 fundout SUCCESS，CMF 通道=ZAND201，SP+VS 行齐全，余额正确扣减
- TC-002：路由至 ZAND203，SP 返回 ZIT 开头 ChannelRefId，VS 后状态变 S，手续费(如 157.50 AED) 入账
- TC-003：BMOC 审批后触发 ZAND204，境内快速完成
- TC-004：BMOC 审批后触发 ZAND207，VS 到达后置 S
- TC-005：ZAND210 通道，境内 ~12 秒
