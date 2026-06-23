---
id: domain_kyc
object_type: Domain
name: kyc
aliases: [KYC, 实名认证]
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md + UAT Kibana trace
tags: [KYC, 实名认证, EID, Passport]
related_services: [svc_kyc, svc_kyc_service]
---

# kyc(实名认证)

> 业务域总览。owner xinwei.cao。本页是 kyc 域的入口节点,细节见各服务/接口对象。

## 概述
KYC(Know Your Customer / 实名认证)业务域:对用户做身份核验,支撑
**EID(阿联酋身份证)** 与 **Passport(护照)** 两类实名认证 journey——OCR 识别 →
活体核身(liveness)→(必要时)人工审核 → 结果回传,并覆盖续期(renew)、换绑手机、
放弃、重验/重拍等分支。下游依赖会员(member)、风控(acs)等。

## 覆盖范围
- EID 认证 journey、Passport 认证 journey、续期 renew、换绑手机、KYC 状态/信息查询。
- 部署 APP:`gp078_kyc`(主,33 接口)、`gp202_kyc-service`。

## 关联关系
- **关键服务**:[[svc_kyc]](gp078,实名认证核心,33 接口)、[[svc_kyc_service]](gp202)
- **下游依赖**:[[svc_member]] 会员、[[svc_acs]] 风控、[[svc_outman]](见各服务正文)
- **关键流程**:待补(可挂 §9 登录/KYC/绑卡 回归链)
- **自动化资产**:[[auto_kyc_eid_journey]]、[[auto_kyc_profile]](cgs-apitest 回归)

## QA 关注点
- 两条 journey 的正常 / 异常分支:OCR 失败、活体失败重拍、人审 vs 免审、EID/护照过期、放弃不可重提。
- VIP 敏感字段脱敏(`******`);未认证活体的 `mobile` 密文传参。
- signzy 临时通道(passport v2)已暂停——回归注意。
- 更多测试重点 / 已知坑 **待补**。
