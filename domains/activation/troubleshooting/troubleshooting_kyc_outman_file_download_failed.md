---
id: ts_kyc_outman_file_download_failed
object_type: Troubleshooting
domain: activation
status: active
owner: xinwei.cao
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-24'
source_type: kibana
source_ref: UAT Kibana app_id=kyc / mClass=OutmanClientImpl / ERROR，7d 窗口(2026-06-24)观测 38 次(KYC 唯一高频硬 ERROR)
tags:
- kyc
- outman
- 文件下载
- 依赖
subdomain: biz-record
module: null
sensitivity: normal
name: outman 文件下载失败(outman.file_download_failed)
aliases:
- outman.file_download_failed
- KycClientException file download
related_services:
- svc_kyc
- svc_outman
related_tables:
- tbl_kyc_tr_biz_record_ocr
- tbl_kyc_tr_biz_record_live
- tbl_kyc_tr_biz_record_passport_live
related_scenarios:
- scn_kyc_eid_full_journey
related_logs:
- service:kyc
- service:outman
related_failures: []
---

# outman 文件下载失败(outman.file_download_failed)

## 症状
Kibana(app_id=kyc,mClass=`c.u.k.e.i.outman.impl.OutmanClientImpl`,**ERROR**)出现:
`系统异常 com.uaepay.kyc.domain.biz.vo.KycClientException: outman.file_download_failed`。
**7 天观测 38 次,是 KYC 唯一高频的硬 ERROR**(其余 ERROR 多为基础设施 ping/启动)。

## 关联关系
- **涉及服务 / 表**:[[svc_kyc]] →(下游)[[svc_outman]];读写 [[tbl_kyc_tr_biz_record_ocr]] / [[tbl_kyc_tr_biz_record_live]] / [[tbl_kyc_tr_biz_record_passport_live]] 的图片 tag/文件名
- **相关日志**:`service:kyc`(OutmanClientImpl ERROR)、`service:outman`(下游侧)
- **关联场景**:[[scn_kyc_eid_full_journey]](OCR / 活体 / 人脸比对取图)

## 可能根因
KYC 向 **outman(文件 / 影像存储服务,KYC 下游 5062 次/7d)** 下载 OCR / 活体 / 证件图片失败:
- outman 侧文件**不存在 / 已过期 / 被清理**(file tag 失效)。
- **跨环境 file tag**:用了别的环境的图片 tag(自动化常见)。
- outman 服务**波动 / 超时**,瞬时不可用。

## 排查步骤(DB/Kibana)
1. Kibana:app_id=`kyc`,mClass.keyword=`c.u.k.e.i.outman.impl.OutmanClientImpl`,mLevel=`ERROR`,
   关键字 `outman.file_download_failed`,取出失败的 **file tag / 文件名**。
2. DB 定位该图片来源:
   ```sql
   select record_id, req_front_file_name, req_back_file_name from tr_biz_record_ocr where ...;
   -- 活体:tr_biz_record_live.req_image_package_tag / req_check_image_name
   -- 护照活体:tr_biz_record_passport_live.req_image_package_tag
   ```
3. 对照 **outman 服务日志**(service:outman)确认是文件不存在还是服务异常。

## 处理 / 规避
- **QA**:确认图片 file tag **有效且属当前环境**;不要跨环境复用图片 tag。
- 可构造**文件缺失 / 过期**的异常场景,验证取图失败时流程的降级 / 报错是否合理。
- 若 outman 服务波动:属下游依赖可用性问题,KYC 侧应有重试 / 友好报错。
> 这是 KYC 对 outman 的**强依赖点**——outman 不稳直接打断 OCR/活体环节。
