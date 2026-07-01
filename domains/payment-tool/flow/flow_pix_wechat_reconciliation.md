---
id: flow_pix_wechat_reconciliation
object_type: Flow
name: PIX 微信渠道对账文件下载与自动对账流程
aliases: [微信对账, pix-wechat reconciliation]
domain: payment-tool
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/433881954
tags: [pix, wechat, reconciliation, 对账]
related_services: []
related_tables: []
related_scenarios: [scn_pix_wechat_vendor_api]
---

# PIX 微信渠道对账文件下载与自动对账流程

## 概述
微信渠道对账文件需通过特定 vendor API 下载。流程由 pix 调用 vendor `QUERY_BILL_ADDRESS`(Requester)下载对账文件,经 ufs 保存后将 `fileTag` 写入 DB(DB 只保存 fileTag,非文件本体);reconciliation 服务通过自动对账 job 调度,回调 pix 拿到 fileTag 后从 ufs 读取文件内容执行自动对账。文件下载与对账解耦。
服务对象 svc_pix 待补。

## 步骤(跨系统)
1. **download check file**(Time → pix):pix → vendor(Tenpay)`get file address`(`QUERY_BILL_ADDRESS`)→ pix upload 文件至 ufs;DB 保存 `fileTag`。
2. **auto reconciliate**(Time → reconciliation):reconciliation 配置自动对账 job,定义 dubbo api。
   - 2.1 get file:reconciliation → pix(返回 fileTag);pix → ufs 读取文件内容。

## 关联关系
- **经过的服务(有序)**:pix(pix-wechat)→ vendor(Tenpay)/ ufs;reconciliation → pix(服务对象待补)
- **关键场景 / 参考**:[[scn_pix_wechat_vendor_api]]
- **主流程**:[[flow_pix_wechat_mpc_payment]]

## 校验点
- 对账文件下载必须通过 vendor `QUERY_BILL_ADDRESS` 场景 API。
- 文件保存路径为 ufs,DB 中只保存 fileTag。
- reconciliation 与 pix 通过 dubbo api 交互,job 周期与对账配置由 reconciliation 侧维护。
- Owner:auto reconciliate 由 Yibin Xia 负责;download check file 步骤 Owner 待补。
