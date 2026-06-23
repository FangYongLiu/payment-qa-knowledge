---
id: api_kyc_passport_submit_v2
object_type: API
domain: kyc
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:89009c95-2642-4856-b64c-da186d7ed287
tags:
- signzy
- 暂停
- 2025-10-10新增
subdomain: passport
module: null
sensitivity: normal
name: 提交护照信息接口(v2)
aliases: []
related_services: []
related_tables: []
related_scenarios:
- passport-kyc-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
提交护照识别信息（v2）。用于下线 mblink、使用 signzy 代替的临时方案。2025-10-10 新增，方案暂停。

## 路径/方法
- 路径：`/kyc/passport/v2/submit-passport`

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
原文未提供。非200不返回业务响应。

## 测试校验点
- 必填字段校验：token、passportNo、passportAvatarTag、fullName、birthday、gender、expiryDate、nationality、ocrServiceProvider、industry。
- 选填字段：passportType、issueDate、issuePlace 可不传。
- ocrServiceProvider 应为 signzy（signzy 临时替代 mblink 方案）。
- nextStep 取值范围：PP_OCR、PP_LIVENESS、AUDIT、DOWN；典型样例为 PP_LIVENESS。
- 与 v1 接口（`/kyc/passport/v1/submit-passport`）的差异：v2 不再传 passportPageTag，仅传 passportAvatarTag。
- 方案暂停状态下接口可用性确认。
