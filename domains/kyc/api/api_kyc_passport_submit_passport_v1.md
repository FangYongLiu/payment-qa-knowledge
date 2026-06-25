---
id: api_kyc_passport_submit_passport_v1
object_type: API
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/205914971
tags:
- passport
- kyc
- microblink
subdomain: passport
module: null
sensitivity: normal
name: 提交护照识别信息接口(v1)
aliases: []
related_services:
- svc_kyc
related_tables:
- tbl_kyc_tm_biz_record
- tbl_kyc_tr_biz_record_passport
related_scenarios: []
---

## 用途
提交护照识别信息（microblink方案），属于护照KYC认证流程中OCR识别完成后的信息提交步骤。

## 关联关系
- **所属服务**:[[svc_kyc]](related_services;api→service 边)
- **读写的表**:待补
- **被哪些场景测**:§9 登录/KYC 回归(待补具体 scenario 对象)

## 路径/方法
- 路径：/kyc/passport/v1/submit-passport

## 入参
业务请求：

| 名称 | 类型 | 非空 | 描述 | 样例 |
|---|---|---|---|---|
| token | String | Y | 认证流程token | |
| passportPageTag | String | Y | 护照页tag | |
| passportAvatarTag | String | Y | 护照头像tag | |
| passportNo | String | Y | 护照编号密文 | |
| passportType | String | N | 护照类型 | |
| fullName | String | Y | 姓名密文 | |
| birthday | String | Y | 生日（yyyy-MM-dd） | |
| gender | String | Y | 性别 0:女，1:男 | |
| expiryDate | String | Y | 有效期（yyyy-MM-dd） | |
| issueDate | String | Y | 签发日期（yyyy-MM-dd） | |
| nationality | String | Y | 国籍code, 三位 | CHN |
| industry | String | Y | 行业 | Retail |
| ocrServiceProvider | String | Y | ocr识别渠道 | microblink |

## 出参
业务响应（非200则不返回）：

| 名称 | 类型 | 非空 | 描述 | 样例 |
|---|---|---|---|---|
| nextStep | String | Y | 下一步骤：PP_OCR / PP_LIVENESS / AUDIT / DOWN | PP_LIVENESS |
| tips | String | Y | 返回文案 | |

## 错误码
原文未列出具体错误码，仅说明非200则不返回业务响应。

## 测试校验点
- token 必传且与流程一致；
- 必填字段（passportPageTag、passportAvatarTag、passportNo、fullName、birthday、gender、expiryDate、issueDate、nationality、industry、ocrServiceProvider）缺失时校验拒绝；
- passportType 可为空；
- 日期字段格式 yyyy-MM-dd；
- gender 取值仅 0/女、1/男；
- nationality 为三位国籍code（如 CHN）；
- ocrServiceProvider 固定为 microblink；
- 成功后 nextStep 应为 PP_LIVENESS（或根据流程为 AUDIT、DOWN），并返回 tips 文案；
- 非200场景不返回业务响应体。
