---
id: ts_outman_ufs_download_fail
object_type: Troubleshooting
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-24'
source_type: kibana
source_ref: UAT Kibana app_id=outman / mClass=UfsServiceClientImpl + SignzyOcrChannel / ERROR，7d 观测 ~13.7 万次
tags: [payment-core, outman, 文件下载, UFS, OCR]
subdomain: file-service
module: null
sensitivity: normal
name: outman 文件处理失败 — UFS 下载 & Signzy OCR(outman)
aliases: [outman.file_download_failed, UFS download process fail, SignzyOcrChannel]
related_services: [svc_outman, svc_kyc]
related_tables: []
related_scenarios: []
related_logs: [service:outman]
related_failures: [ts_kyc_outman_file_download_failed]
---

# outman 文件处理失败 — UFS 下载 & Signzy OCR(outman)

## 症状
Kibana(app_id=outman,ERROR,7 天约 13.7 万次):
- `UfsServiceClientImpl`(~11 万):`OutMan-->UFS download process fail ... OutmanException: outman.file_download_failed`。
- `SignzyOcrChannel`(~2.7 万):Signzy OCR 通道异常。

## 关联关系
- **涉及服务**:[[svc_outman]](文件/影像服务)→ UFS 文件存储;为 [[svc_kyc]] 等提供取图
- **相关日志**:`service:outman`(UfsServiceClientImpl / SignzyOcrChannel)
- **关联故障**:[[ts_kyc_outman_file_download_failed]](KYC 侧调 outman 取图失败,本条是 outman→UFS 的下游侧)

## 可能根因
- **outman→UFS 下载失败**:UFS 上文件不存在/已过期/key 失效/跨环境 tag;UFS 服务波动。
- **Signzy OCR 通道异常**:OCR 第三方通道波动/证件质量差。
- 是 KYC 取图失败([[ts_kyc_outman_file_download_failed]])的**下游根因侧**——KYC 看到的 `outman.file_download_failed` 多半源于此。

## 排查步骤(DB/Kibana)
1. Kibana:app_id=`outman`,mClass.keyword=`...UfsServiceClientImpl`,关键字 `outman.file_download_failed`,取失败的 file key。
2. 核对 UFS 上该文件是否存在/有效;跨环境 tag?
3. OCR 类:看 SignzyOcrChannel 错误详情(通道/证件)。

## 处理 / 规避
- **QA**:确认图片/文件 key 有效且属当前环境(自动化勿跨环境复用 file tag);可构造文件缺失异常场景。
- 业务侧:UFS 下载失败退避重试 + 明确错误码;与 KYC 侧 [[ts_kyc_outman_file_download_failed]] 联动定位。
> 与 KYC 排障对象互为上下游,排查时一并看。
