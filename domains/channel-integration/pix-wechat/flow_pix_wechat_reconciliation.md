---
id: flow_pix_wechat_reconciliation
object_type: Flow
domain: channel-integration
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:a68e3cf4-694f-4d32-9a67-4b4aaeee8675
tags:
- reconciliation
- wechat
- pix
- mpc
subdomain: pix-wechat
module: reconciliation
sensitivity: normal
name: PIX微信对账文件处理流程
aliases: []
related_services: []
related_tables: []
related_scenarios:
- QUERY_BILL_ADDRESS
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
PIX微信MPC渠道的对账文件需要通过指定的Vendor API主动下载，下载后通过ufs存储，并由reconciliation服务调度自动对账Job完成对账处理。

## 步骤(跨系统)

| Step | System | Function | Take care | Owner |
|---|---|---|---|---|
| 1 download check file | pix | 通过 vendor api 下载对账文件，并通过 ufs 保存文件；将 fileTag 保存到 db | - | TODO |
| 2 auto reconciliate | reconciliation | 配置自动对账 Job；定义 dubbo api | TODO | Yibin Xia |
| 2.1 get file | pix | 返回 fileTag | - | TODO |

## 涉及服务/表
- 服务：pix(pix-wechat)、reconciliation、ufs
- Vendor API：`QUERY_BILL_ADDRESS`(Requester，下载对账文件地址)
- 持久化：对账文件存储于 ufs；fileTag 落库

## 校验点
- 下载到的对账文件需通过 ufs 保存，并将 fileTag 持久化以便后续查询
- reconciliation 服务通过 dubbo api 从 pix 获取 fileTag 后再获取文件进行自动对账
- 自动对账 Job 的调度配置由 reconciliation 端完成
