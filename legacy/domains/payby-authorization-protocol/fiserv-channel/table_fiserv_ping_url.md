---
id: tbl_fiserv_ping_url
object_type: Table
domain: payby-authorization-protocol
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:529d83bb-f8c0-47a4-af94-b05017e2e750
tags:
- fiserv
- ping_url
- routing
subdomain: fiserv-channel
module: null
sensitivity: normal
name: fiserv.t_ping_url
aliases: []
related_services: []
related_tables:
- tbl_fiserv_out_bound
related_scenarios:
- scn_fiserv_test_env_mock_tid
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储 Fiserv 渠道绑定过程中获取到的 ping_url 及其连通性 response time，用于后续交易报文路由。
- 在渠道绑定流程中：qpay-fsii 通过 register_url 注册 TID 后，会得到 4 个 ping_url；qpay-fsii 分别 ping 这 4 个 URL 确保能通，并把 ping 的 response time 保存到本表。
- 在交易流程中：qpay-fsii 收到交易请求后，从 `fiserv.t_ping_url` 里找速度最快的那个(response_time_ms 最小的)URL，请求该 URL 发送交易报文。
- 有效期约束：Fiserv 要求每 6 小时重新获取一次 ping_url，所以系统只会把 `update_time` 在最近 6 小时之内的 URL 作为有效的 ping_url。

## 关键列
- ping_url：注册 register_url 后由 Fiserv 返回的 4 个 URL 之一，用于发送交易报文。
- response_time_ms：qpay-fsii ping 该 URL 的响应耗时，用于路由时挑选最快的 URL。
- update_time：记录刷新时间，用于判断 ping_url 是否仍在 6 小时有效期内。

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 渠道绑定成功后，本表应有该 TID 对应的 4 条 ping_url 记录，且 response_time_ms 已写入。
- 仅 `update_time` 在最近 6 小时之内的记录才被视为有效；超过 6 小时应重新获取 ping_url，否则交易路由会使用过期 URL。
- 交易请求来到 qpay-fsii 时，应选用 response_time_ms 最小的 ping_url 发送交易报文。
- 测试环境通常使用 mock(因 Fiserv 测试环境 TID 配置可能被改动导致交易失败)，因此本表数据是否真实与 Fiserv 联通需结合环境判断。
