---
id: api_kyc_passport_submit_ocr
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
- ocr
- signzy
subdomain: passport
module: null
sensitivity: normal
name: 提交护照OCR接口(signzy临时方案)
aliases: []
related_services:
- svc_kyc
related_tables:
- tbl_kyc_tm_biz_record
- tbl_kyc_tr_biz_record_passport
related_scenarios: []
---

## 用途
提交护照OCR识别信息，用于下线mblink，使用signzy代替的临时方案（2025-10-10新增，方案暂停）。

## 关联关系
- **所属服务**:[[svc_kyc]](related_services;api→service 边)
- **读写的表**:待补
- **被哪些场景测**:§9 登录/KYC 回归(待补具体 scenario 对象)

## 路径/方法
- 路径：/kyc/passport/v1/submit-ocr

## 入参
业务请求：

| 名称 | 类型 | 非空 | 描述 |
|---|---|---|---|
| token | String | Y | 认证流程token |
| passportPageTag | String | Y | 护照页tag |

## 出参
业务响应（非200则不返回）：

| 名称 | 类型 | 非空 | 描述 | 样例 |
|---|---|---|---|---|
| nextStep | String | Y | 下一步骤：PP_OCR / PP_SUBMIT / PP_LIVENESS / AUDIT / DOWN | PP_SUBMIT |
| passportNo | String | Y | 护照编号密文 | |
| passportType | String | N | 护照类型 | |
| passportAvatarTag | String | Y | 护照头像 | |
| fullName | String | Y | 姓名密文 | |
| birthday | String | Y | 生日（yyyy-MM-dd） | |
| gender | String | Y | 性别 0:女，1:男 | |
| expiryDate | String | Y | 有效期（yyyy-MM-dd） | |
| issueDate | String | N | 签发日期（yyyy-MM-dd） | |
| issuePlace | String | N | 签发地 | |
| nationality | String | Y | 国籍code, 三位 | CHN |
| ocrServiceProvider | String | Y | ocr识别渠道 | signzy |

## 错误码
原文未提供。

## 测试校验点
- 入参 token、passportPageTag 必填校验。
- 响应 nextStep 取值范围：PP_OCR、PP_SUBMIT、PP_LIVENESS、AUDIT、DOWN；正常流转下应为 PP_SUBMIT。
- 响应 ocrServiceProvider 应为 signzy（区别于 v1/submit-passport 的 microblink）。
- 必填字段校验：passportNo、passportAvatarTag、fullName、birthday、gender、expiryDate、nationality 不为空。
- 可选字段：passportType、issueDate、issuePlace 允许为空。
- 非200响应不返回业务体。
- 该接口为临时方案，注意方案暂停状态下的可用性确认。
