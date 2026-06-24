---
id: ts_ppc_compensation_customer_exists
object_type: Troubleshooting
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-24'
source_type: kibana
source_ref: UAT Kibana app_id=ppc / mClass=CompensationEventExecutorImpl / ERROR，7d 观测 ~9 万次
tags: [payment-core, ppc, 补偿事件, 幂等]
subdomain: ppc
module: null
sensitivity: normal
name: 补偿事件执行异常 — Customer id already exists(ppc)
aliases: [执行事件异常, 613-Customer id already exists, CompensationEventExecutor]
related_services: [svc_ppc, svc_member]
related_tables: []
related_scenarios: [scn_wallet_consumer_pay]
related_logs: [service:ppc]
related_failures: []
---

# 补偿事件执行异常 — Customer id already exists(ppc)

## 症状
Kibana(app_id=ppc,mClass=`CompensationEventExecutorImpl`,ERROR):
`执行事件异常 ErrorException: 613-Customer id already exists`。**7 天观测约 9 万次。**

## 关联关系
- **涉及服务**:[[svc_ppc]](PPC 交易)→ [[svc_member]](客户/账户)
- **相关日志**:`service:ppc`(CompensationEventExecutorImpl)
- **关联场景**:[[scn_wallet_consumer_pay]]

## 可能根因
- 补偿事件(失败重试)在创建客户时撞到 **`613-Customer id already exists`**——客户**已存在**,但补偿仍按"新建"重放。
- 本质是**幂等问题**:补偿应识别"已存在=视为成功/跳过",而非重复创建报错并不断重试(故高频)。

## 排查步骤(DB/Kibana)
1. Kibana:app_id=`ppc`,mClass.keyword=`...CompensationEventExecutorImpl`,关键字 `Customer id already exists`,看是哪个事件/customer。
2. 核对补偿事件表(execute_status/execute_count)是否在反复重试同一已存在客户。
3. 确认下游 member 侧该 customer 确实已存在。

## 处理 / 规避
- **QA**:验证补偿幂等——"客户已存在"应被当作成功/幂等跳过,不应无限重试刷 ERROR。
- 业务侧:补偿执行器对 `613-already exists` 做幂等处理(视为成功并终止重试)。
> 高频且持续,典型**补偿幂等缺陷**信号,建议优先确认。
