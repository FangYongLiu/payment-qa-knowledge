---
id: ts_kyc_nationality_not_found
object_type: Troubleshooting
domain: kyc
status: active
owner: xinwei.cao
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-24'
source_type: kibana
source_ref: UAT Kibana app_id=kyc / mClass=KycNationNamesServiceImpl / WARN，7d 窗口(2026-06-24)观测 342 次
tags:
- kyc
- 国籍
- 别名表
- 数据修复
subdomain: reference
module: null
sensitivity: normal
name: 获取不到国籍信息(国籍别名表缺写法)
aliases:
- 获取不到国籍信息
- nationality not found
related_services:
- svc_kyc
related_tables:
- tbl_kyc_tm_nationality_alias
related_scenarios: []
related_logs:
- service:kyc
related_failures: []
---

# 获取不到国籍信息(国籍别名表缺写法)

## 症状
Kibana(app_id=kyc,mClass=`c.u.k.d.m.s.i.KycNationNamesServiceImpl`,WARN)出现:
`获取不到国籍信息：United Arab Emirates (the)`。**7 天观测 342 次。**
通道返回的国籍写法在别名表里匹配不到 → 国籍归一化失败。

## 关联关系
- **涉及服务 / 表**:[[svc_kyc]] / [[tbl_kyc_tm_nationality_alias]](`nationality_alias` / `nationality_name` / `short_name_alpha3`)
- **相关日志**:`service:kyc`(mClass=KycNationNamesServiceImpl,关键字 `获取不到国籍信息`)

## 可能根因
- 通道返回的是 **ISO 标准全称带后缀**(如 `United Arab Emirates (the)`、`Korea (the Republic of)`),
  而 [[tbl_kyc_tm_nationality_alias]] 的 `nationality_alias` 里**没有收录这种 "(the)" 后缀写法**。
- ⚠️ 命中的恰是 **UAE 本地用户(主力市场)**,影响面不小。

## 排查步骤(DB/Kibana)
1. DB 确认别名表是否缺该写法:
   ```sql
   select id, nationality, nationality_name, nationality_alias, short_name_alpha3, channel
   from tm_nationality_alias
   where nationality_alias like '%United Arab Emirates%'
      or nationality_name like '%United Arab Emirates%';
   ```
2. Kibana:app_id=`kyc`,mClass.keyword=`c.u.k.d.m.s.i.KycNationNamesServiceImpl`,关键字 `获取不到国籍信息`,收集所有未命中的国籍字符串。

## 处理 / 规避
- **数据修复(可直接行动)**:给 [[tbl_kyc_tm_nationality_alias]] 对应 UAE 记录(`short_name_alpha3=ARE`)的
  `nationality_alias` 补上 `United Arab Emirates (the)` 等带 "(the)" 后缀的 ISO 写法;
  按 Kibana 收集到的全量未命中字符串批量补别名(注意按 `channel` 维度)。
- **QA 回归**:用国籍为 `United Arab Emirates (the)`(及其它 "(the)" 后缀国家)的证件做实名,
  验证归一化命中、`short_name_alpha3` 正确落库。
> 建议把"通道国籍写法 vs 别名表覆盖"做成持续巡检(Kibana 周期跑该关键字)。
