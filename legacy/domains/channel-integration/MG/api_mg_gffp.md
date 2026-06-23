---
id: api_mg_gffp
object_type: API
domain: channel-integration
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:AQ/1268547712
tags:
- MG
- 信息收集
- 动态字段
subdomain: mg
module: info-collection
sensitivity: normal
name: MG信息字段查询接口 (GFFP)
aliases:
- GFFP
- Get Form Fields
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
返回指定收款国家+币种下，汇款需要收集的所有信息字段。系统比对数据库已有字段，如缺少则在页面动态展示补充输入框。

## 路径/方法
- 接口名：GFFP (Get Form Fields)
- 渠道：MG (MoneyGram)，间接渠道

## 入参
- 收款国家
- 币种

（原文未列出更多详细参数）

## 出参
返回该国家+币种下汇款需要收集的所有字段列表。

（原文未列出具体字段结构）

## 错误码
原文未提供。

## 测试校验点
- 调用时机：用户进入 Transfer Details 页面时调用
- 缓存逻辑：24小时内只调用一次，结果存入缓存，之后从缓存取
- 字段比对：返回字段需与数据库已有字段比对，缺失字段需在页面动态展示补充输入框
- 不同国家返回字段差异较大，需验证多国家+币种组合
- 缓存过期（>24小时）后应重新调用接口
