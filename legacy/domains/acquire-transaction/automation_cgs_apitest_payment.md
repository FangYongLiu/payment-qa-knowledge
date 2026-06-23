---
id: auto_cgs_apitest_payment
object_type: AutomationAsset
domain: acquire-transaction
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-22'
source_type: code_repo
source_ref: code_repo:caa31aee-5510-525f-9def-2ec2ccce0d9a
tags:
- automation
- pytest
- payment
- kyc
- member
- acquire
- mpgs
subdomain: null
module: payment
sensitivity: normal
name: cgs-apitest payment 自动化测试模块
aliases:
- cgs-apitest/testcases/payment
related_services: []
related_tables: []
related_scenarios:
- scn_mpgs_directpay_3ds2
- scn_mpgs_moto_payment
- scn_mpgs_device_pay
- scn_mpgs_cardorg_split
- scn_mpgs_refund_void
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`cgs-apitest` 仓库 `payment` 模块的自动化测试资产入口，commit `f723c15efa81770245eabfe37e702c99695fa2da`。该模块作为受 BimoQA 视作权威的"团队已显式验证行为"的来源，覆盖 PayBy 钱包/收单/会员/KYC 端到端关键链路。

- **覆盖文件**：`testcases/payment` 下 77 个文件，其中 52 个测试文件 + 25 个被引用的封装/工具源码（由 import 自动跟随）。
- **覆盖业务域**：
  - 会员侧：KYC EID Journey、Passport KYC、Profile 浏览（多 KYC 等级）、绑/解卡、绑/解 IBAN、登录、注册、注销、支付密码（设置/修改/忘记/收银台首设）、账单查询、Profile/付款码资料展示。
  - 资金侧：扣款顺序（付款码 / AutoDebit）、账户余额查询、ZAND IBAN 分配。
  - 收单侧：MPGS 渠道 DirectPay 3DS2、MOTO 免 3DS、设备支付（ApplePay / GooglePay / SamsungPay）、卡组织拆分路由（PAYBY MC / NI VISA）、AD 两阶段（Authorize→Capture）+ Void、全额/部分退款。

## 使用方式

- **目录入口**：`testcases/payment`。
- **执行框架**：`pytest`，按 `@pytest.mark.regression` / `@pytest.mark.uat` / `@pytest.mark.sim` 标签筛选。
- **公共 Fixtures**（多数文件采用 `autouse=True` 的 `setup`）：
  - `get_env` / `get_urls`：取 `cgs_url`、`sgs_url`。
  - `get_env_data`：环境配置。
  - `db_instance_factory(role)`：按角色返回 `select` / `member` / `dpm` / `protocol` / `tradeii` 等库连接，支持 `select_sql` 与 `execute_sql`。
  - `get_testdata`：YAML 驱动，按测试方法名取参数化数据集。
  - `get_redis_conf`：支付密码相关用例清理 `gp005_member`、`PayPwdValidate` 缓存。
  - `skip_if_not_uat`：CKO 等仅 UAT 用例。
- **核心封装**：
  - `API.payment_api.module.Module`：组合业务动作（`login` / `payby_login` / `bind_card` / `bind_iban` / `remove_bank_card` / `remove_bank_account` / `create_non_kyc_user` / `get_kyc_user` / `create_zand_kyc_user` / `get_zand_kyc_user` / `deposit_submit` / `cashdesk_pay` / `cashdesk_pay_password`）。
  - `API.payment_api.cgs.CGSapi`：CGS 接口封装（personal/cashdesk/risk/ups/grc/cashier/ptp/mock_3ds 等）。
  - `API.payment_api.SGS.SGS`：SGS 受理网关封装（`acquire2_placeOrder` / `acquire2_getOrder`）。
  - `utils.RSA.RSA_encrypt`：手机号 / 卡数据 RSA 加密、随机 token 生成。
  - `utils.sendDubbo.call_dubbo_service`：Dubbo 调用（如 `IMemberKycFacade.queryKycInfo`）。
  - `utils.pay_password_utils.clear_pay_password`、`utils.redis_utils`：支付密码清理。
  - `MPGS3DS2Client(env).complete_3ds2_authentication(threeDs_id)`：模拟 MPGS 3DS2 持卡人验证。

## 关键配置

- **统一支付密码**：`132580`。
- **商户密钥**：`acs.t_key_config` 按 PARTNER_ID + `CERT_TYPE='PRIVATE'` + `enable_flag='Y'` 取 `RELATE_CERT`，用于 RSA 加密卡四要素。
- **商户产品要求**：MPGS 用例要求商户开通 Auto Debit、Direct Pay Domestic Card、Direct Pay INTL Card；TC019/TC020 商户为 Lottery 业务并配置卡组织分流策略到 MPGS202/MPGS204。
- **预置数据**：
  - KYC FINISH 用户：通过 `kyc.tm_kyc_apply` SQL submit 预置（nationality=India、industry=Technology）。
  - ZAND IBAN 白名单：用户需在 `VISII_KYC_MID_WHITELIST`（示例 `1TZHXRCM` / `100000091371`）。
  - CKO 用例：通过 SQL 直改 `dpm.t_dpm_outer_account` 状态与子账户余额至 1000。
- **关键表交互**：
  - 会员：`member.tm_member`、`member.tm_member_identity`、`member.tr_password`、`member.tm_operator`、`member.tr_bank_account`、`member.tr_deduct_channel`、`member.tr_beneficiary_info`、`member.tr_member_preference`、`member.tr_verify_ref`。
  - KYC：`kyc.tm_kyc_apply`。
  - 注销：`memberfront.t_member_logout_reason`、`memberfront.t_apply`。
  - 协议：`protocol.t_contract_sign_info`。
  - 资金：`dpm.t_dpm_outer_account`、`dpm` 子账户表。
  - 收单：`acquireii.t_acquire_order`、`tradeii.t_trade_order`、`cmf.tt_cmf_order`、`cmf.tt_inst_order`、`cmf.tt_inst_order_result`。
- **路由约束**：MPGS DirectPay 同步响应 `status=CREATED`；3DS2 触发凭 `body.interActionParams.threeDSecureDom` 中 `/3ds2/page/<id>` 正则提取 threeDs_id；MOTO 用例反向断言不应包含 `threeDSecureDom`；订单终态 `acquireOrder.status ∈ {PAID_SUCCESS, SETTLED}`，trade 表 `trade_status='SS'`，cmf 主单 `STATUS='S'`。

## 注意事项

- 多个核心 KYC EID journey 用例（`test_kyc_eid_check_reminder` / `test_kyc_eid_inquire_info_finish` / `test_kyc_eid_inquire
