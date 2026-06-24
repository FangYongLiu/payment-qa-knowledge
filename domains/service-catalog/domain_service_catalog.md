---
id: domain_service_catalog
object_type: Domain
name: service-catalog
aliases: [待认领, 未归属, 中性区, uncategorized, unclaimed]
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-24'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [service-catalog, 待认领, 未归属]
related_services: []
---

# service-catalog(待认领 / 未归属服务中性区)

> **这不是业务域**,而是**「待认领」中性区**:还没有明确业务域/团队归属的服务骨架暂存于此。
> 由 `scripts/import_services.py` 生成并每次重建;认领后移到对应 `domains/<domain>/`。
> 名字 `service-catalog` = 全量服务骨架认领区(沿用,脚本写死,勿改名)。

## 这里放什么
- 没有明确负责人(dev_owner = Unknown / 空)或暂未归属业务域的服务。
- 多为基础设施边缘、Mock、第三方渠道占位、历史遗留等。
- ⚠️ 留在此处**不影响知识图谱**——服务仍可被图遍历(只要有调用边/表/API 等关系);
  domain 只是软路由+归属标签。有了明确归属再认领即可。

## 当前分组(subdomain,便于人看懂;非正式业务域)
- `mock`:mock-datawire、pns-merchant-mocker
- `member-account`:user-profile-scheduler、customer-service、officer
- `transaction`:pcbs、pws、rtp
- `risk-compliance`:afis、palm-id
- `merchant-portal`:adg
- `marketing`:youstore-installment
- `misc`:agreements-static、tpay-nyu、asite、tld-service、exchange-rate-crawler、kiosk-mgmt

## 认领方式
确认负责人/业务域后:改服务 frontmatter `domain` + `owner`/`reviewer`(域 lead)+ `dev_owner`,
并把文件移到 `domains/<domain>/`(参考 `docs/SERVICE_DOMAIN_CLAIM.md`)。
