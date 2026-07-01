---
id: domain_activation
object_type: Domain
name: activation
aliases: [KYC, 实名认证]
domain: activation
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

### 三个验证渠道(channel)
用户走哪个渠道取决于其证件类型与选择(资金类操作 top-up/transfer/remittance 前必须先完成 KYC):

| Channel | 证件 | 底层 provider | 适用人群 | 状态 |
|---|---|---|---|---|
| **UAEKYC** | Emirates ID (EID) | 官方 UAE API | 大多数用户(主渠道) | ACTIVE |
| **UAE Pass** | EID(经 UAE Pass App) | UAE Pass(政府数字身份) | 偏好 UAE Pass 验证的用户 | ACTIVE |
| **Passport** | 护照 | Signzy | 无 EID 的 WPS workers | ACTIVE |

## 关联关系
- **关键服务**:[[svc_kyc]](gp078,实名认证核心,33 接口)、[[svc_kyc_service]](gp202)
- **下游依赖(UAT Kibana 7d 实测 + 频次)**:[[svc_member]] 会员(8.4万,最重)、[[svc_outman]] 文件/影像(5062)、[[svc_acs]] 风控(996)、[[svc_mns_main]] 消息(470)、bps(6)、[[svc_pts]](4)
- **上游调用方(谁调 kyc,7d 实测)**:`member-front`(1.7万)、`grc-check-identity-provider`(1608,风控身份核验)、`personal`(1072)、[[svc_mssii]](788)、`member`(272)
- **关键流程**:[[flow_kyc_passport]](护照 KYC 端到端)、[[flow_kyc_eid_renew]](EID 续期)、[[flow_kyc_change_mobile]](换绑手机);EID 主 journey 见 [[scn_kyc_eid_full_journey]]。
- **自动化资产**:[[auto_kyc_eid_journey]]、[[auto_kyc_profile]](cgs-apitest 回归)
- **数据表(kyc 库,36 张)**:主单 [[tbl_kyc_tm_kyc_apply]]、业务记录基础 [[tbl_kyc_tm_biz_record]] + 各环节明细 `tr_biz_record_*`(OCR/活体/ICA/验证/护照/换绑/地址/客户详情/依赖/人脸比对);人工审核 [[tbl_kyc_tm_audit_task]]/log;通知 `tm_notify_record`/`tm_message_*`;过期事件 [[tbl_kyc_tm_eid_expiry_notify_event]]/`tm_pp_expiry_notify_event`;风控名单 `t_eid_fraudlist`/`t_face_blacklist*`;生命周期 `tm_kyc_activity_log`/`tm_remove_kyc_reason`/[[tbl_kyc_tr_leave_record]];发号/补偿 `leaf_alloc`/`t_compensation_event`。详见 `domains/kyc/table_kyc_*.md`。

## QA 关注点
- 两条 journey 的正常 / 异常分支:OCR 失败、活体失败重拍、人审 vs 免审、EID/护照过期、放弃不可重提。
- VIP 敏感字段脱敏(`******`);未认证活体的 `mobile` 密文传参。
- signzy 临时通道(passport v2)已暂停——回归注意。
- **数据落库校验**:`tm_kyc_apply.token` 贯穿全程,与各 `tr_biz_record_*.req_token` 必须一致;`status`/`current_status`(PROCESS→FINISH)流转 + `success_time` 仅成功写;敏感字段(idn/eid/护照号/手机/人脸)密文落库。
- **已知坑(UAT Kibana 实测)**:[[ts_kyc_no_exist_record]](查询用错/过期 token,2003次/7d)、[[ts_kyc_ocr_date_null_out_of_range]](OCR 有效期/出生日期空或越界,1029次)、[[ts_kyc_nationality_not_found]](国籍别名表缺 "(the)" 后缀写法,UAE 高频,342次)、[[ts_kyc_outman_file_download_failed]](调 outman 取图失败,唯一硬 ERROR,38次)。
- 预期行为(非坑,勿当 bug):通知限频(`同类通知已超限`)、删 EID 时 `eidTicket` 为空。

## 环境 / 接入(URL 配置)
> 整合自 legacy env-urls;供前端/配置中心/联调查阅。业务方:CashNow / Botim / PayBy。

- **CGS API 域名**:SIM `https://sim.test2pay.com/cgs/api`;UAT/PROD 见配置中心。所有 CGS 接口 `POST` + JSON。
- **域名规律**:SIM/UAT `https://uat-identity.test2pay.com`;PROD `https://identity.botim.money`。
- **KYC 入口**(`/kyc/home?pbw_show_title=N&partner=<方>`)、**活体入口**(`/biometric?...&partner=<方>`)、**回调**(`/broadcast.html`,即 `redirecturl`)按 partner(cashnow/botim/payby)区分;Botim MP 走小程序协议 `https://botim.me/mp/b/?app=me.botim.pay.kyc`。
- 活体 v2(`/kyc/body-auth/v2/liveness/apply`)的 `videoUrl` 由配置 `applyUrlV2` 与 signzy url 拼接;Botim MP 活体的 `${signzy_url}` 占位由后端 URL-encode 后拼入。
- **术语**:CGS = Client Gateway Service(客户端网关服务),KYC/支付各业务方接入的统一客户端网关。

## 流程 / 场景 / 排障 索引
本域 流程 / 场景 / 排障 / 自动化 对象索引:
- [[auto_kyc_eid_journey]](自动化:KYC EID Journey 端到端自动化 (test_KYC_eid_journey))
- [[auto_kyc_profile]](自动化:KYC 用户 Profile 查看自动化 (test_KYC_xinwei))
- [[flow_kyc_change_mobile]](流程:KYC 换绑手机号端到端流程 (Change Mobile))
- [[flow_kyc_eid_renew]](流程:EID 续期端到端流程 (EID Renew))
- [[flow_kyc_passport]](流程:护照 KYC 认证端到端流程 (Passport KYC))
- [[scn_kyc_eid_full_journey]](场景:EID 完整实名认证 journey (NON→FINISH))
- [[scn_kyc_eid_leave]](场景:放弃 EID 认证 journey)
- [[scn_kyc_profile_view]](场景:KYC 认证 Profile 查看(各用户类型))
- [[scn_kyc_status_inquire]](场景:KYC 状态查询与提醒 (FINISH / NON / reminder))
- [[scn_kyc_zand_iban]](场景:KYC 用户分配 ZAND IBAN)
- [[ts_kyc_nationality_not_found]](排障:获取不到国籍信息(国籍别名表缺写法))
- [[ts_kyc_no_exist_record]](排障:KYC 查询返回 NO_EXIST_RECORD(记录不存在))
- [[ts_kyc_ocr_date_null_out_of_range]](排障:OCR 有效期/出生日期为空或越界(日期解析告警))
- [[ts_kyc_outman_file_download_failed]](排障:outman 文件下载失败(outman.file_download_failed))
