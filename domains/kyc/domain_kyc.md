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
- **下游依赖(UAT Kibana 7d 实测 + 频次)**:[[svc_member]] 会员(8.4万,最重)、[[svc_outman]] 文件/影像(5062)、[[svc_acs]] 风控(996)、[[svc_mns_main]] 消息(470)、bps(6)、[[svc_pts]](4)
- **上游调用方(谁调 kyc,7d 实测)**:`member-front`(1.7万)、`grc-check-identity-provider`(1608,风控身份核验)、`personal`(1072)、[[svc_mssii]](788)、`member`(272)
- **关键流程**:待补(可挂 §9 登录/KYC/绑卡 回归链)
- **自动化资产**:[[auto_kyc_eid_journey]]、[[auto_kyc_profile]](cgs-apitest 回归)
- **数据表(kyc 库,36 张)**:主单 [[tbl_kyc_tm_kyc_apply]]、业务记录基础 [[tbl_kyc_tm_biz_record]] + 各环节明细 `tr_biz_record_*`(OCR/活体/ICA/验证/护照/换绑/地址/客户详情/依赖/人脸比对);人工审核 [[tbl_kyc_tm_audit_task]]/log;通知 `tm_notify_record`/`tm_message_*`;过期事件 [[tbl_kyc_tm_eid_expiry_notify_event]]/`tm_pp_expiry_notify_event`;风控名单 `t_eid_fraudlist`/`t_face_blacklist*`;生命周期 `tm_kyc_activity_log`/`tm_remove_kyc_reason`/[[tbl_kyc_tr_leave_record]];发号/补偿 `leaf_alloc`/`t_compensation_event`。详见 `domains/kyc/table_kyc_*.md`。

## QA 关注点
- 两条 journey 的正常 / 异常分支:OCR 失败、活体失败重拍、人审 vs 免审、EID/护照过期、放弃不可重提。
- VIP 敏感字段脱敏(`******`);未认证活体的 `mobile` 密文传参。
- signzy 临时通道(passport v2)已暂停——回归注意。
- **数据落库校验**:`tm_kyc_apply.token` 贯穿全程,与各 `tr_biz_record_*.req_token` 必须一致;`status`/`current_status`(PROCESS→FINISH)流转 + `success_time` 仅成功写;敏感字段(idn/eid/护照号/手机/人脸)密文落库。
- **已知坑(UAT Kibana 实测)**:[[ts_kyc_no_exist_record]](查询用错/过期 token,2003次/7d)、[[ts_kyc_ocr_date_null_out_of_range]](OCR 有效期/出生日期空或越界,1029次)、[[ts_kyc_nationality_not_found]](国籍别名表缺 "(the)" 后缀写法,UAE 高频,342次)、[[ts_kyc_outman_file_download_failed]](调 outman 取图失败,唯一硬 ERROR,38次)。
- 预期行为(非坑,勿当 bug):通知限频(`同类通知已超限`)、删 EID 时 `eidTicket` 为空。
