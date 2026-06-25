---
id: ts_kyc_ocr_date_null_out_of_range
object_type: Troubleshooting
domain: kyc
status: active
owner: xinwei.cao
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-24'
source_type: kibana
source_ref: UAT Kibana app_id=kyc / mClass=KycBizRecordConverter / WARN，7d 窗口(2026-06-24)观测 1029 次(KYC 第二高频)
tags:
- kyc
- OCR
- 日期解析
- 数据质量
subdomain: eid
module: null
sensitivity: normal
name: OCR 有效期/出生日期为空或越界(日期解析告警)
aliases:
- expiryDate null
- birthDate null
- 时间日期为空或超过最大范围
related_services:
- svc_kyc
related_tables:
- tbl_kyc_tr_biz_record_ocr
- tbl_kyc_tr_biz_record_ica
- tbl_kyc_tm_eid_expiry_notify_event
related_scenarios:
- scn_kyc_eid_full_journey
related_logs:
- service:kyc
related_failures: []
---

# OCR 有效期/出生日期为空或越界(日期解析告警)

## 症状
Kibana(app_id=kyc,mClass=`c.u.k.d.m.c.KycBizRecordConverter`,WARN)出现:
`expiryDate:null：时间日期为空或超过最大范围`、`birthDate:null：时间日期为空或超过最大范围`。
**7 天观测 1029 次,是 KYC 第二高频告警。** 转换器据此丢弃该日期字段(落库为 null)。

## 关联关系
- **涉及服务 / 表**:[[svc_kyc]] / [[tbl_kyc_tr_biz_record_ocr]]、[[tbl_kyc_tr_biz_record_ica]](`ocr_expiry_date` / `ocr_birth_date` / `req_date_of_birth`)
- **下游影响**:[[tbl_kyc_tm_eid_expiry_notify_event]](过期判断依赖有效期)
- **相关日志**:`service:kyc`(mClass=KycBizRecordConverter,关键字 `时间日期为空或超过最大范围`)
- **关联场景**:[[scn_kyc_eid_full_journey]]

## 可能根因
- OCR / 通道(signzy / ICA)**未识别出**有效期 / 出生日期(证件模糊、反面未拍全、MRZ 不清)。
- 通道返回的日期**格式越界**:空串、`0000-00-00`、超出 `datetime` 可表示范围。
- 字段映射时源值非法,`KycBizRecordConverter` 主动丢弃 → 落库 null。

## 排查步骤(DB/Kibana)
1. DB 看该笔记录的日期字段是否落空:
   ```sql
   select id, record_id, ocr_expiry_date, ocr_birth_date, resp_code, resp_msg
   from tr_biz_record_ocr where record_id = '<record_id>';
   -- ICA 侧:tr_biz_record_ica.req_date_of_birth / ica_eid_expiry_date
   ```
2. Kibana:app_id=`kyc`,mClass.keyword=`c.u.k.d.m.c.KycBizRecordConverter`,关键字 `时间日期为空或超过最大范围`,定位 record。

## 处理 / 规避
- **QA 关注**:这是**数据质量边界**,不是崩溃。需验证:日期为空时流程**不应异常中断**,而应转人审 / 提示重拍重提,且 EID/护照**过期判断**对 null 有效期有兜底(不能误判为已过期或永久有效)。
- 构造**模糊证件 / 缺有效期**的用例,覆盖 OCR 识别失败分支。
> 偶发(证件质量)属预期;若某通道/某类证件**持续**触发,需查通道 OCR 解析逻辑。
