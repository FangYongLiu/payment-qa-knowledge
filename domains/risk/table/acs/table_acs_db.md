---
id: tbl_acs_db
object_type: Table
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/124289264
tags:
- 网关
- 权限
- 白名单
subdomain: gateway
module: null
sensitivity: normal
name: 网关库(acs)核心表
aliases:
- acs
related_services:
- svc_acs
---

## 用途
acs 库存放网关层的配置数据，覆盖公私钥配置、接口权限、接口分组、接口分组关系以及 IP 白名单等网关核心配置。

## 关键列
- `acs.t_key_config`：公私钥配置
- `acs.t_gateway_merchant_api_auth`：接口权限
- `acs.t_gateway_api_group`：接口配置
- `acs.t_gateway_api_group_relation`：接口分组关系
- `acs.t_reffer_list`：IP 白名单

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 排查接口调用鉴权问题时，确认 `t_gateway_merchant_api_auth` 中商户对应接口权限是否开通。
- 接口分组归属问题，需联查 `t_gateway_api_group` 与 `t_gateway_api_group_relation`。
- 报文加解签异常，核对 `t_key_config` 中的公私钥配置。
- 调用方 IP 被拒，检查 `t_reffer_list` 中 IP 白名单是否登记。
