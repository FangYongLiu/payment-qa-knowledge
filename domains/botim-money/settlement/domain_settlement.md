---
id: domain_settlement
object_type: Domain
name: settlement
aliases: [清结算, reconciliation, 对账, counter, 结算]
domain: settlement
business_line: botim-money
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
dev_owner: yibing.xia
last_reviewed_at: '2026-06-26'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [settlement, 清结算, 对账]
related_services: [svc_reconciliation, svc_counter, svc_commission, svc_pcbs]
---

# settlement(清结算)

> 域入口。清算、结算、对账。owner xiaoyan.zhou / 研发 Payment Core(Yibing Xia)/ 运营 Clearing & Settlement 团队(Zhaohui Liu)。

## 概述
资金的清算与对账:对账文件生成与差异检测(reconciliation)、结算与结算后台(counter)、佣金计算(commission)、余额/账务报表(pcbs)、复式记账账务库(dpm)。MPGS 商户直连结算等。

## 本域内容
- **service/** — reconciliation、counter、commission、pcbs。
- **table/** — reconciliation(对账)、dpm(账务/复式记账)。

## 相邻域
渠道对账 → [[domain_payment_tool]];交易核心 → [[domain_payment_core]];出款 → [[domain_fundout]];入款 → [[domain_deposit_vam]]。
