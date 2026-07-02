---
id: auto_kyc_eid_journey
object_type: AutomationAsset
name: KYC EID Journey 端到端自动化 (test_KYC_eid_journey)
aliases: [TestKYCEidJourney, test_KYC_eid_journey]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/basic_cases/test_KYC_eid_journey.py
tags: [KYC, EID, 实名认证, ZAND, IBAN, 自动化, cgs-apitest]
related_scenarios: [scn_kyc_eid_full_journey, scn_kyc_eid_leave, scn_kyc_status_inquire, scn_kyc_zand_iban]
related_services: [svc_kyc]
related_tables: [tbl_member_tr_member_kyc_level]
---

# KYC EID Journey 端到端自动化

> 来源:cgs-apitest 回归套件 `test_KYC_eid_journey.py`(`TestKYCEidJourney`,11 个 TC)。
> 覆盖新建 NON-KYC 用户 → 走完 EID 实名认证 journey → KYC FINISH,并延伸到 ZAND IBAN 分配。

## 用途
对 **EID(阿联酋身份证)实名认证 journey** 做端到端回归——从"未认证用户(NON)"
一路验证到"认证完成(FINISH)",再到钱包/ZAND IBAN 开通。覆盖的 11 个用例:

| TC | 用例 | 覆盖点 |
| --- | --- | --- |
| 1 | check_reminder | 已完成 KYC 用户的提醒确认 → [[api_kyc_check_reminder]] |
| 2 | inquire_info(FINISH) | 已认证用户查 KYC 状态,含 eidInfo/passportInfo → [[api_kyc_inquire_info]] |
| 3 | inquire_info(NON) | 新建 NON-KYC 用户查状态=NON |
| 4 | start_journey | NON 用户启动 EID journey,返回 token/moveForward → [[api_kyc_eid_start_journey]] |
| 5 | inquire_industry | 行业列表非空 → [[api_kyc_eid_inquire_industry]] |
| 6 | **full_journey** | NON→KYC 全链:login→验 NON→start→get_result→选行业→confirm→验完成→DB 校验 → [[api_kyc_eid_get_result]] · [[api_kyc_eid_confirm_info]] |
| 7 | leave_journey | 带原因放弃 journey → [[api_kyc_eid_leave_submit]] |
| 8 | get_kyc_user | 复用预置 KYC FINISH mock 用户(零手工),验 eidInfo(India/Technology)+ DB |
| 9 | create_non_kyc_user | 静默注册全新 NON 用户(全自动) |
| 10 | e2e_new_user_to_zand_iban | 新用户→KYC FINISH→分配 ZAND IBAN→钱包 ACTIVATED(全自动) |
| 11 | zand_iban_assigned | 白名单 KYC 用户(VISII_KYC_MID_WHITELIST)验 ZAND IBAN 已分配 |

## 关联关系
- **覆盖的场景**:[[scn_kyc_eid_full_journey]]、[[scn_kyc_eid_leave]]、[[scn_kyc_status_inquire]]、[[scn_kyc_zand_iban]]
- **针对/跑在的服务**:[[svc_kyc]](实名认证核心);延伸触达 member(账户)、personal/钱包、ZAND(visii VA)。
- **调用的接口**:见上表各 `api_kyc_*` 接口链接;ZAND 段用 `vam_auth_init/query_info`、钱包用 `personal_sva_queryStatusInfo`(非 kyc 服务接口)。

## 使用方式
- 框架:pytest + allure;入口 `pytest testcases/payment/basic_cases/test_KYC_eid_journey.py`。
- markers:`regression` / `sim` / `uat`(按环境/套件筛选)。
- 依赖夹具(`setup`):`get_env`、`get_urls`(cgs_url/sgs_url)、`get_env_data`、`db_instance_factory`、`get_testdata`;
  业务封装 `Module`(login / create_non_kyc_user / get_kyc_user / create_zand_kyc_user / get_zand_kyc_user)、`CGSapi`、`ZandMigrationCGS`。
- 测试数据:`get_testdata` 按方法名取(如 `test_kyc_eid_full_journey` 的 partner_id/uid/mobile_no/industry/except_msg)。

## 关键配置
- **DB 校验表**(`db_instance_factory('select')`):
  - `member.tr_member_kyc_level`(kyc_level=2 / status=VALID 表示认证有效)
  - `kyc.tm_kyc_apply`(TC8 mock 用户一次性 submit SQL 预置)
  - `visii.t_va`(ZAND 虚拟账户:status='V' / iban / account_type)
- 真实 Signzy 实体 + `vam_auth_active` bypass(TC10);TC11 固定真实用户 `1TZHXRCM`(member 100000091371)。

## 注意事项
- **环境差异**:SIM 环境 Signzy journey 自动完成;**UAT 需在 start-journey 与 get-result 之间手工完成 Signzy**。
- TC8/9/10 设计为**零手工全自动**(mock 用户 + 静默注册 + bypass),适合常驻回归;TC6 full_journey 在 UAT 受 Signzy 手工步骤限制。
- get_result 的 `commandType` 决定渲染分支(action=成功带 eidInfo / 其他);断言依赖 `except_msg` 文案。
- 更多 flaky/数据坑 **待补**。
