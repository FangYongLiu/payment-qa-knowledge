---
id: svc_kyc
object_type: Service
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp078
layer: 风控/合规/KYC
name: kyc
dev_owner: 沈纲领
aliases: [gp078_kyc]
related_services: [svc_member, svc_outman, svc_acs, svc_pts]
related_tables: []
related_scenarios: []
---

# kyc

> 来源:UAT Kibana trace(宽窗口)+ 接口文档整合。app_group=`gp078` · domain=`kyc` · dev_owner=沈纲领。

## 作用
实名认证(KYC)核心服务:支撑 **EID(阿联酋身份证)** 与 **Passport(护照)** 两类实名认证 journey
——OCR 识别 → 活体核身(liveness)→(必要时)人工审核 → 结果回传,并覆盖续期(renew)、换绑手机、
放弃、重验/重拍等流程分支。下游调 member(账户)、acs(风控)、outman;被 merchant-frontend 调用。

## 系统中的位置
- 功能层:风控 / 合规 / KYC
- 业务域:`kyc`(owner xinwei.cao / dev 沈纲领)

## 关联关系
**调用(下游):** [[svc_member]] 会员账户(188462 次)、[[svc_outman]](11206)、[[svc_acs]] 风控(5046)、[[svc_pts]](4)。
**被调用(上游):** merchant-frontend。

## 涉及的 API / 接口
实名认证两条 journey + 通用查询,共 33 个接口(每个的**完整规格——路径/入参/出参/错误码/校验点——见对应接口对象**):

**① EID(身份证)认证 journey**
- 启动:[[api_kyc_eid_start_journey]]
- 确认 / 修改:[[api_kyc_eid_confirm_info]](无修改→免审)、[[api_kyc_eid_submit_edit]](有修改→人审)、[[api_kyc_eid_inquire_industry]](选行业)
- 重验 / 重拍:[[api_kyc_eid_verify_again]]、[[api_kyc_eid_get_retake_selfie_result]]
- 取结果:[[api_kyc_eid_get_result]](commandType 渲染 成功/失败/审核中/EID 过期)
- 续期 renew:[[api_kyc_eid_renew_start_journey]]、[[api_kyc_eid_renew_confirm_info]]、[[api_kyc_eid_renew_submit_edit]]、[[api_kyc_eid_renew_verify_again]]、[[api_kyc_eid_renew_retake_selfie]]、[[api_kyc_eid_renew_get_result]]、[[api_kyc_eid_renew_leave_submit]]
- 换绑手机:[[api_kyc_eid_confirm_change_mobile]]、[[api_kyc_confirm_change_mobile]]
- 放弃:[[api_kyc_eid_leave_submit]](记录原因,不可重提)

**② Passport(护照)认证 journey**
- 启动 / 初始化:[[api_kyc_passport_start_journey]]、[[api_kyc_passport_init]]
- 提交 OCR:[[api_kyc_passport_submit]]、[[api_kyc_passport_submit_passport_v1]](microblink);[[api_kyc_passport_submit_ocr]]、[[api_kyc_passport_submit_v2]]、[[api_kyc_passport_submit_passport_v2]](signzy 临时,2025-10 新增,**已暂停**)
- 活体:[[api_kyc_passport_liveness]]、[[api_kyc_passport_retake_selfie]]
- 确认 / 取结果 / 放弃:[[api_kyc_passport_confirm_info]]、[[api_kyc_passport_get_result]]、[[api_kyc_passport_verify_again]]、[[api_kyc_passport_leave_submit]]

**③ 通用 / 查询**
- [[api_kyc_inquire_info]](查 KYC 状态 + EID/护照信息,VIP 脱敏 `******`)、[[api_kyc_check_reminder]](提醒确认 EID)、[[api_kyc_body_unauth_apply]](未登录基于手机号密文申请活体)

## 涉及的数据库表
- **待补**:本服务读写的表本窗口未观测到、接口文档未提供,留待人工补充。

## 关键方法 / 入口
- 对外入口:上列 33 个 HTTP 接口(EID / Passport 两条 journey + 通用查询)。
- Dubbo / RPC 方法级(mClass)本窗口未单独抽取——**待补**。

## 测试要点 / 排障(待补)
- 两条 journey 的正常/异常分支:OCR 失败、活体失败重拍、人审 vs 免审、EID/护照过期、放弃不可重提。
- VIP 敏感字段脱敏(`******`);未认证活体的 `mobile` 密文传参。
- **更多待人工补充**(具体校验点、已知 bug、排障路径)。

## 参与的业务场景(cgs 回归)
- §9. 登录 / KYC / 绑卡(`test_login` / `test_*eid*` / `test_bankcards`)
- **自动化资产**:[[auto_kyc_eid_journey]](EID 认证 journey 端到端)、[[auto_kyc_profile]](各状态用户 Profile 查看)

## 来源与置信
- **下游调用 + 频次**:UAT Kibana 宽窗口 trace(observed,高置信)。
- **接口清单(33)**:接口文档整合(高置信),含已暂停项(passport signzy v2)。
- **数据库表 / Dubbo 方法级 / 具体校验点**:本窗口未观测,标**待补**,留人工补充。
