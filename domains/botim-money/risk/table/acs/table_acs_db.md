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
related_tables:
- tbl_acs_db
- tbl_acs_leaf_alloc
- tbl_acs_t_api_config
- tbl_acs_t_api_mgr
- tbl_acs_t_api_mgr_group
- tbl_acs_t_basic_group
- tbl_acs_t_gateway_api_config
- tbl_acs_t_gateway_api_group
- tbl_acs_t_gateway_api_group_relation
- tbl_acs_t_gateway_merchant_api_auth
- tbl_acs_t_group_relation
- tbl_acs_t_key_config
- tbl_acs_t_language_config
- tbl_acs_t_merchant_api_auth
- tbl_acs_t_merchant_api_support
- tbl_acs_t_merchant_config_template
- tbl_acs_t_merchant_fo_setting
- tbl_acs_t_merchant_funds
- tbl_acs_t_merchant_inner_account
- tbl_acs_t_merchant_key
- tbl_acs_t_merchant_setting
- tbl_acs_t_operation_config
- tbl_acs_t_outer_code
- tbl_acs_t_rate_limit_config
- tbl_acs_t_rate_limit_group
- tbl_acs_t_reffer_list
- tbl_acs_t_setting_attribute
- tbl_acs_t_template_account
- tbl_acs_t_template_auth
- tbl_acs_t_template_auth_group
- tbl_acs_t_translate_config
- tbl_acs_t_unity_code_mapping
- tbl_acs_t_wh_key
- tbl_acs_t_withhold_auth
- tbl_acs_t_withhold_auth_log
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
