---
id: svc_kyc_service
object_type: Service
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp202
layer: 风控/合规/KYC
name: kyc-service
dev_owner: Gangling.Shen
aliases: [gp202_kyc-service]
related_services: [svc_member]
related_tables: []
related_scenarios: []
---

# kyc-service

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp202` · domain=`kyc`。

## 作用
实名认证服务（EID journey，调 member）

## 系统中的位置
- 功能层:风控 / 合规 / KYC (Risk / Compliance / KYC)
- 业务域:`kyc`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 21344 次 · high

**被调用(上游)—— 这些服务调用本服务:**
aml, basis

## 涉及的 API / 数据库表
- **暴露/相关 API**:**待补**(本服务的接口清单本窗口未抽取;注意区别于 [[service_gp078_kyc]] 的 33 个接口——二者是不同 APP)。
- **读写的表**:**待补**。

## 关键方法 / 入口
- 实名认证(EID journey)相关方法;具体入口 / mClass **待补**。

## 测试要点 / 排障(待补)
- 与 [[service_gp078_kyc]] 的职责边界(为何拆两个 APP)**待补**确认。
- 更多校验点 / 已知坑留人工补充。

## 参与的业务场景(cgs 回归)
- §9. 登录 / KYC / 绑卡(basic_cases:`test_login` / `test_*eid*` / `test_bankcards`)

## 来源与置信
- **下游调用 + 频次**:UAT Kibana 120d 宽窗口 trace(observed,候选待人审)。
- **作用 / API / 表 / 方法**:大部分**待补**——本服务观测稀,需 owner(xinwei.cao)/ dev(Gangling.Shen)确认。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。
