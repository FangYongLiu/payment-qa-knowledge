---
id: ts_kyc_no_exist_record
object_type: Troubleshooting
domain: kyc
status: active
owner: xinwei.cao
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-24'
source_type: kibana
source_ref: UAT Kibana app_id=kyc / mClass=ResponseUtil / WARN，7d 窗口(2026-06-24)观测 2003 次(KYC 最高频告警)
tags:
- kyc
- 错误码
- NO_EXIST_RECORD
- 查询
subdomain: core
module: null
sensitivity: normal
name: KYC 查询返回 NO_EXIST_RECORD(记录不存在)
aliases:
- No exist record
- NO_EXIST_RECORD
related_services:
- svc_kyc
related_tables:
- tbl_kyc_tm_kyc_apply
related_scenarios:
- scn_kyc_status_inquire
related_logs:
- service:kyc
related_failures: []
---

# KYC 查询返回 NO_EXIST_RECORD(记录不存在)

## 症状
调用 get-result / inquire-info / confirm-info 等**查询类接口**时返回业务异常,错误码 `NO_EXIST_RECORD`。
Kibana(app_id=kyc,mClass=`c.u.kyc.core.common.utils.ResponseUtil`,WARN)出现
`No exist record 业务异常,错误码:NO_EXIST_RECORD`。**7 天观测 2003 次,是 KYC 最高频告警。**

## 关联关系
- **涉及服务 / 表**:[[svc_kyc]] / [[tbl_kyc_tm_kyc_apply]](按 `token` 查不到流程主单)
- **相关日志**:`service:kyc`(mClass=ResponseUtil,关键字 `NO_EXIST_RECORD`)
- **关联场景**:[[scn_kyc_status_inquire]]

## 可能根因
- 用**错误 / 过期的 token** 查询(token 与 [[tbl_kyc_tm_kyc_apply]].`token` 对不上)。
- journey **尚未创建**(未先 start-journey)就调 get-result / inquire-info。
- 测试用例 **token 跨用例 / 跨用户 / 跨环境复用**——这是自动化回归里最常见的诱因。
- 对应 apply 已被清理 / 删除(见 [[tbl_kyc_tm_remove_kyc_reason]] / 活动日志)。

## 排查步骤(DB/Kibana)
1. DB 确认主单是否存在及状态:
   ```sql
   select id, member_id, token, status, current_status, create_time
   from tm_kyc_apply where token = '<token>';
   ```
   查不到 → token 无效 / 未创建;查到但状态异常 → 看 current_status。
2. Kibana:app_id=`kyc`,mClass.keyword=`c.u.kyc.core.common.utils.ResponseUtil`,关键字 `NO_EXIST_RECORD`,定位是哪个接口、哪个 token。

## 处理 / 规避
- **QA 回归**:每个用例先 start-journey 拿到**当次有效 token** 再做后续查询;token 不跨用例复用;跨环境不复用 token。
- 业务侧:查询前应有 token 有效性校验,NO_EXIST_RECORD 属预期的"无记录"提示(非系统故障)。
> 该错误码本身是**业务校验**结果,不是系统异常;高频出现多为测试数据/token 使用方式问题。
