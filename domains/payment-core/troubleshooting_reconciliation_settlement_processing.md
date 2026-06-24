---
id: ts_reconciliation_settlement_processing
object_type: Troubleshooting
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-24'
source_type: kibana
source_ref: UAT Kibana app_id=reconciliation / ZandRpsEscrowProcessor + RouteSftpMethodProcessor / ERROR，7d 观测 ~91 万次
tags: [payment-core, reconciliation, 对账, 结算, SFTP]
subdomain: reconciliation
module: null
sensitivity: normal
name: 对账/结算处理异常 — 重复结算明细 & SFTP 对账下载(reconciliation)
aliases: [Exist Processing SettlementDetail, RouteSftpMethodProcessor, 对账下载]
related_services: [svc_reconciliation]
related_tables: []
related_scenarios: []
related_logs: [service:reconciliation]
related_failures: []
---

# 对账/结算处理异常 — 重复结算明细 & SFTP 对账下载(reconciliation)

## 症状
Kibana(app_id=reconciliation,ERROR,7 天约 91 万次),两类高频:
- `crowAdjustStrategyZandRpsEscrowProcessor`(~58 万):`Exist Processing SettlementDetail`(结算明细已在处理中/重复)。
- `RouteSftpMethodProcessor`(~22 万):SFTP 对账文件下载(如 `fundChannelCode=NIPOS101`,`billDate=...`)。
- `AutoSettlementServiceImpl`(~10 万)。

## 关联关系
- **涉及服务**:[[svc_reconciliation]](对账/清结算)
- **相关日志**:`service:reconciliation`(ZandRpsEscrowProcessor / RouteSftpMethodProcessor / AutoSettlementServiceImpl)

## 可能根因
- **重复结算明细**:`Exist Processing SettlementDetail` —— 同一结算明细被重复处理(并发/重跑/幂等),处理器抛已存在。
- **SFTP 对账下载**:按渠道(NIPOS101 等)按日下载对账文件失败——文件未生成/未到/凭证或路径问题。
- 多为**定时任务(daemon/Job)反复重试**导致高频。

## 排查步骤(DB/Kibana)
1. Kibana:app_id=`reconciliation`,分别按 `ZandRpsEscrowProcessor` / `RouteSftpMethodProcessor` 关键字,取 billDate / fundChannelCode / 结算明细 id。
2. SFTP 类:核对该渠道该日对账文件是否已生成/可下载;凭证/路径。
3. 重复明细类:核对结算明细处理状态,是否并发/重跑导致重复。

## 处理 / 规避
- **QA**:对账/结算多为定时批处理,UAT 高频常因渠道文件缺失/重跑——回归时关注**幂等**与**文件到达**。
- 业务侧:重复明细幂等跳过;SFTP 下载失败退避重试 + 告警,不刷 ERROR。
> 量级高且以定时任务为主,先区分"渠道文件未到"vs"真实结算错误"。
