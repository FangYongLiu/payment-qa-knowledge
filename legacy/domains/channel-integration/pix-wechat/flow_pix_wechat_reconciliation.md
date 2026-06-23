---
id: flow_pix_wechat_reconciliation
object_type: Flow
domain: channel-integration
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/433881954
tags:
- reconciliation
- wechat
- pix
subdomain: pix-wechat
module: reconciliation
sensitivity: normal
name: 微信渠道对账文件下载与对账流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
微信渠道的对账文件需通过特定 vendor API 下载。流程由 pix 调用 vendor API 拉取对账文件，经 ufs 保存后将 fileTag 写入 DB；reconciliation 服务通过自动对账 job 调度，回调 pix 拿到 fileTag 后执行自动对账。

对应 Vendor API 场景：`Requester: QUERY_BILL_ADDRESS`(download reconciliation file)。

## 步骤(跨系统)

| Step | System | Function |
|---|---|---|
| 1 download check file | pix | Download file with vendor api and save it via ufs；Save the fileTag to db |
| 2 auto reconciliate | reconciliation | Config auto reconciliate job；Define dubbo api |
| 2.1 get file | pix | Return the fileTag |

## 涉及服务/表
- pix(pix-wechat)：调用 vendor API `QUERY_BILL_ADDRESS` 下载对账文件；通过 ufs 持久化文件；DB 中保存 fileTag；对外提供 dubbo 接口返回 fileTag
- ufs：对账文件存储
- reconciliation：自动对账 job 调度方，定义 dubbo api，按周期回调 pix 获取 fileTag 完成对账

## 校验点
- 对账文件下载必须通过 vendor 的 `QUERY_BILL_ADDRESS` 场景 API 完成
- 文件保存路径为 ufs，DB 中只保存 fileTag(而非文件本体)
- reconciliation 与 pix 之间通过 dubbo api 交互，job 周期与对账配置由 reconciliation 侧维护
- Owner：auto reconciliate 由 Yibin Xia 负责；download check file 步骤 Owner TODO
