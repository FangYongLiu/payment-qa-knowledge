---
id: api_kyc_passport_submit_passport_v2
object_type: API
domain: kyc
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/205914971
tags:
- passport
- kyc
- signzy
- v2
subdomain: passport
module: null
sensitivity: normal
name: 提交护照信息接口(v2)
aliases: []
related_services: []
related_tables: []
related_scenarios:
- kyc-passport-auth-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
提交护照识别信息，用于下线 mblink，使用 signzy 代替的临时方案（2025-10-10 新增，方案暂停）。

## 路径/方法
- 路径：/kyc/passport/v2/submit-passport

## 入参
业务请求：

| 名称 | 类型 | 非空 | 描述 | 样例 |
|---|---|---|---|---|
| token | String | Y | 认证流程token |  |
| passportNo | String | Y | 护照编号密文 |  |
| passportType | String | N | 护照类型 |  |
| passportAvatarTag | String | Y | 护照头像 |  |
| fullName | String | Y | 姓名密文 |  |
| birthday | String | Y | 生日（yyyy-MM-dd） |  |
| gender | String | Y | 性别 0:女，1:男 |  |
| expiryDate | String | Y | 有效期（yyyy-MM-dd） |  |
| issueDate | String | N | 签发日期（yyyy-MM-dd） |  |
| issuePlace | String | N | 签发地 |  |
| nationality | String | Y | 国籍code, 三位 | CHN |
| ocrServiceProvider | String | Y | ocr识别渠道 | signzy |
| industry | String | Y | 行业 | Retail |

## 出参
业务响应（非200则不返回）：

| 名称 | 类型 | 非空 | 描述 | 样例 |
|---|---|---|---|---|
| nextStep | String | Y | 下一步骤：PP_OCR / PP_LIVENESS / AUDIT / DOWN | PP_LIVENESS |
| tips | String | Y | 返回文案 |  |

## 错误码
原文未提供。

## 测试校验点
- token 必传，须为有效的认证流程 token。
- passportNo、passportAvatarTag、fullName、birthday、gender、expiryDate、nationality、ocrServiceProvider、industry 均为必传字段；passportType、issueDate、issuePlace 可空。
- ocrServiceProvider 取值为 signzy（区别于 v1 的 microblink）。
- nationality 必须为三位国籍 code（如 CHN）。
- 与 v1 (/kyc/passport/v1/submit-passport) 区别：v2 不再传 passportPageTag；新增 issuePlace；issueDate 改为非必填。
- 响应 nextStep 取值集合：PP_OCR、PP_LIVENESS、AUDIT、DOWN，正常流转下一步为 PP_LIVENESS。
- 非 200 不返回业务响应。
- 注意该接口为临时方案，目前方案已暂停。
