---
id: scn_online_business_zand_fundout
object_type: Scenario
name: ZAND渠道出款测试场景(TC-001~010)
aliases: [ZAND Fundout 测试用例集, zand-fundout-test-cases]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: wiki:7f334321-3b49-4c87-b6d9-8949925a962a
tags: [online-business, fundout, zand, 测试用例]
related_services: [svc_fundout, svc_cmf, svc_fcw, svc_dpm_accounting, svc_merchant_fundout]
related_tables: [tbl_mhtfundout_t_fundout_order, tbl_mhtfundout_t_fundout_bankcard_order, tbl_cmf_tt_inst_order, tbl_cmf_tt_inst_order_result, tbl_router_t_channel_result_code]
related_logs: []
---

# ZAND渠道出款测试场景(TC-001~010)

## 触发 / 入口
覆盖 ZAND Fundout 业务的 10 条核心测试用例(TC-001 ~ TC-010),触发入口分布于:
- **Merchant Portal**:`uat-web-merchant.test2pay.com`(TC-001, TC-005, TC-006)
- **API 测试框架** cgs-apitest(TC-002, TC-008, TC-009, TC-010)
- **BMOC Counter**:`uat-admin.corp.test2pay.com/counter/`(TC-003, TC-004)
- **Botim App**:Cards & Accounts → Bank Accounts(TC-007)

端到端链路见 [[flow_zand_fundout]];Mock VS 工具见 [[auto_online_business_zand_mock_vs]];排障见 [[ts_zand_fundout]]。

## 关联关系
- **涉及服务**:[[svc_fundout]]、[[svc_cmf]]、[[svc_fcw]]、[[svc_dpm_accounting]]、[[svc_merchant_fundout]](= `related_services`)
- **校验的表**:[[tbl_mhtfundout_t_fundout_order]]、[[tbl_mhtfundout_t_fundout_bankcard_order]]、[[tbl_cmf_tt_inst_order]]、[[tbl_cmf_tt_inst_order_result]]、[[tbl_router_t_channel_result_code]](= `related_tables`)
- **覆盖它的自动化**:[[auto_online_business_zand_mock_vs]](国际单补发 VS)

## 前置条件
- VPN 已连接,可访问 UAT 内部系统。
- DBeaver / SQL Query Portal 可用(查 mhtfundout / cmf / dpm 等库)。DBeaver 只读连接:Host `mysql-rds-uat-pby-aen-001.mysql.database.azure.com`,Port `3306`,账号 `reader` / `cmfuser`。
- 测试账号:
  - `200000086193`(TestABC)— 商户门户境内
  - `200000079033`(0529ZXY01)— 商户门户国际
  - `200000080798`(Test merchant)— API SWIFT
- 测试 IBAN:`AE170961002031010000003`。
- 国际单测试需 Mock VS 工具 `Zand.java`,UAT HMAC key:`CoQnNYbgefTzpvhV1yr8L/Q7RX0m/JjsWMEFmQRFTj8=`,回调 URL:`https://uat-fcw.test2pay.com/fcw/zand/notify`。
- 商户门户转账需「My Authorization」授权;结算流程需 BMOC 审核审批。

## 操作步骤
| TC | 标题(优先级) | 渠道 | 步骤要点 |
|---|---|---|---|
| TC-001 | Domestic transfer via Merchant Portal (P0) | ZAND201 | 登录 Portal(Partner 200000086193)→ Fiat → Transfer → Transfer to Bank → IBAN `AE170961002031010000003` 小额 AED → My Authorization 授权 → 等 ~15s 校验 DB |
| TC-002 | International SWIFT transfer via API (P0) | ZAND203 | `cd cgs-apitest`;`python3 -m pytest testcases/payment/toB/test_placeTransferToBank_fangyong.py::TestPlaceTransferToBank::test_placeTransferToBankOrder_SWIFTUSD -s --env uat` → 等真实 VS 或发 Mock VS |
| TC-003 | Settlement domestic (P1) | ZAND204 | BMOC → Settlement Manage → Settlement Detail → Apply Settlement → Audit → Approve → 校验境内结算 |
| TC-004 | Settlement international (P1) | ZAND207 | 同 TC-003 流程触发国际结算 → 等 VS 或发 Mock VS |
| TC-005 | Merchant portal withdrawal domestic (P1) | ZAND210 | 商户门户 → Fiat → Withdrawal → 本地 UAE 银行 → 确认 → 授权 |
| TC-006 | Merchant portal withdrawal international (P1) | ZAND203 | Partner 200000079033 → Fiat → Withdrawal → 选银行(USD)→ 确认 → 授权 |
| TC-007 | Personal withdrawal via App (P1) | ZAND201 | Botim App → Cards & Accounts → Bank Accounts → 选 ZAND 账户 → Withdraw funds → 确认 |
| TC-008 | Mock VS callback validation (P2) | ZAND203/207 | 从 DB 取 ChannelRefId(`ZIT...`)与 CMF order → 编辑 `Zand.java`(amount/channel_ref/instruction_id)→ 用 UAT HMAC key 编译运行回调 fcw/zand/notify → 校验 VS 行写入 |
| TC-009 | SQ polling flow validation (P2) | ZAND203 | 提交国际单后观察 SQ:SP 后前 ~2 分钟开始,间隔渐增;`RETRY_TIMES>35` 小时级;`RETRY_TIMES=54` 停止 |
| TC-010 | Extension fields consistency SP/SQ/VS (P2) | ZAND203 | 取一条国际单,查 `cmf.tt_inst_order_result` 中 SP/SQ/VS 三行 EXTENSION,校验 CreationDateTime / ChannelRefId / channelTransTime 全程一致 |

## DB 校验点
- `mhtfundout.t_fundout_order`:`status=SUCCESS`,`product_code` 正确(220401/220402/230602),`unity_result_code` 非 `cmf.route.fail`。
- `cmf.tt_inst_order`:`FUND_CHANNEL_CODE` = ZAND201/203/204/207/210,`STATUS=S`,AMOUNT/CURRENCY 正确,`RETRY_TIMES` 行为符合预期。
- `cmf.tt_inst_order_result`:
  - SP 行:`INST_STATUS=I`,`INST_SEQ_NO` 为 `D...`(境内)或 `ZIT...`(国际),EXTENSION 含 CreationDateTime + ChannelRefId + channelTransTime。
  - SQ 行(仅国际):`INST_STATUS=I` 或 `S`,ChannelRefId 与 SP 一致。
  - VS 行(境内):`INST_STATUS=S`,`MEMO=Credited To Beneficiary`,Type=`OUTGOING_DOMESTIC_TRANSACTION_STATUS`。
  - VS 行(国际):`INST_STATUS=S`,`MEMO=PROCESSED`,Type=`OUTGOING_INTERNATIONAL_TRANSACTION_STATUS`。
- `dpm.t_dpm_outer_account_subset`:BALANCE 正确扣减(含手续费,例如国际 SWIFT 157.50 AED)。
- `router.t_channel_result_code`:`PROCESSED` 映射 `result_status=S`。

**常用校验 SQL:**
```sql
-- Fundout 订单状态
SELECT global_id, status, product_code, created_time, unity_result_code
FROM mhtfundout.t_fundout_order
WHERE partner_id = '<partner_id>' ORDER BY global_id DESC LIMIT 5;

-- CMF 渠道订单
SELECT INST_ORDER_NO, FUND_CHANNEL_CODE, STATUS, CURRENCY, AMOUNT, GMT_CREATE
FROM cmf.tt_inst_order
WHERE FUND_CHANNEL_CODE = '<channel>' ORDER BY GMT_CREATE DESC LIMIT 5;

-- SP/SQ/VS 结果轨迹
SELECT INST_ORDER_NO, API_TYPE, INST_STATUS, MEMO, INST_SEQ_NO, EXTENSION, GMT_CREATE
FROM cmf.tt_inst_order_result
WHERE INST_ORDER_NO = '<order>' ORDER BY GMT_CREATE ASC;

-- 商户余额
SELECT BALANCE, CURRENCY FROM dpm.t_dpm_outer_account_subset s
JOIN dpm.t_dpm_outer_account a ON a.ACCOUNT_NO = s.ACCOUNT_NO
WHERE a.MEMBER_ID = '<partner_id>' AND a.ACCOUNT_TYPE = 1
  AND s.BALANCE_TYPE = 1 AND s.fund_type = 1 AND s.CURRENCY = 'AED';
```

## 预期结果
- TC-001:~12s 内 fundout SUCCESS,CMF 通道=ZAND201,SP+VS 行齐全,余额正确扣减。
- TC-002:路由至 ZAND203,SP 返回 `ZIT` 开头 ChannelRefId,VS 后状态变 S,手续费(如 157.50 AED)入账。
- TC-003:BMOC 审批后触发 ZAND204,境内快速完成。
- TC-004:BMOC 审批后触发 ZAND207,VS 到达后置 S。
- TC-005:ZAND210 通道,境内 ~12s。
- TC-006:USD 国际提现走 ZAND203。
- TC-007:个人 App 提现走 ZAND201。
- TC-008~010:Mock VS 写入 VS 行;SQ 轮询行为符合阈值;SP/SQ/VS EXTENSION 一致。
