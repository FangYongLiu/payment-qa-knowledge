---
id: svc_sgs
object_type: Service
domain: online-business
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp028
name: sgs
dev_owner: Yongxing.Cao
aliases: [gp028_sgs]
related_services: [svc_acquireii]
related_tables: []
related_scenarios: [scn_online_business_direct_pay]
---

# sgs

> 来源:UAT Kibana 实测(`java-kafka-logstash-*`,2026-07-03,app_id=`sgs` 近7d 773k docs)+ 作用说明。app_group=`gp028` · domain=`online-business`。

## 作用
**SGS 收单接入网关**(`com.uaepay.gateway.sgs`,基于 ACS)——商户/合作方对外开放 API 的 **HTTPS 入口**(Tomcat `http-nio-8080`)。所有 `/sgs/api/acquire2/*`(下单/查单/退款/撤销/取消/预授权)、`/sgs/api/transfer/*`、话费充值等对外接口先到 sgs,由它**验签、限流、鉴权、加载商户配置后转发给收单核心** [[svc_acquireii]]。是 [[reference_open_api_developer_portal]] 里对外契约的落地网关。

## 系统中的位置
- 功能层:接入网关 / API Gateway(收单对外入口)
- 业务域:`online-business`
- 入口:HTTPS(`http-nio-8080`);服务注册/发现走 Zookeeper(Dubbo);下游收单核心走 Dubbo 调用。

## 关联关系
**下游** —— 转发到收单核心:[[svc_acquireii]](`acquire2` 下单/查单/退款等;经 Dubbo,网关侧未打 `*ClientImpl` 日志,属架构确定边)。
**内嵌 ACS 网关能力**(运行于 sgs 本身,非外部服务):验签、限流、密钥/商户配置、多语言(见下「关键方法」)。

## 涉及的 API / 数据库表
**暴露 / 相关 API:**
- 收单核心:[[api_sgs_acquire_place_order]] / [[api_sgs_acquire_get_order]] / [[api_sgs_acquire_refund_place_order]] / [[api_sgs_acquire_revoke_order]] / [[api_sgs_acquire_cancel_order]] 等 `/sgs/api/acquire2/*`。
- 话费充值:[[api_sgs_place_mobile_order_prepaid]] 预付话费下单接口。
- 协议/枚举字典见 [[reference_acquire_protocol_and_codes]]。

## 关键方法 / 入口(UAT 实测 mClass)
| 类 | 职责 | QA 关联 |
| --- | --- | --- |
| `ReceiveOrderServiceImpl` | 接收对外下单/请求(入口) | 各 `acquire2/*` 入口 |
| `SignServiceImpl` | 请求/响应 **RSA(SHA256WithRSA)验签** | 验签失败 → `403 UNAUTHORIZED` |
| `AcsKeyConfigServiceImpl` | 合作方公钥/密钥配置 | 验签用的 Partner 密钥来源 |
| `AcsRateLimitServiceImpl` | **限流** | 触发 → `402 RATE_LIMIT_REJECT` |
| `AcsMerchantSettingServiceImpl` | 商户配置加载 | 产品未开通/配置校验 |
| `AcsLanguageServiceImpl` | 多语言响应 | `Content-Language` Header |
| `AcsGatewayApiServiceImpl` | 网关 API 编排 | 路由到下游收单 |
| `WriteResponseAssist` / `ServerResponseUtil` / `HandleExceptionAssist` | 响应封装 / 异常处理 | 统一响应体 `head{applyStatus,code,msg,traceCode}` |

## 测试要点 / 排障 / 常见问题
- **验签**:请求与响应都验签(`SignServiceImpl`);错误 sign / 过期 `Partner-Id` / 密钥不匹配 → `403`。用 `AcsKeyConfigServiceImpl` 确认合作方密钥已配。
- **限流**:`AcsRateLimitServiceImpl` 触发 `402 RATE_LIMIT_REJECT`——高频压测/重放用例的预期码。
- **通用前置校验**(所有接口):`requestTime` ±15 分钟、`Partner-Id` ≤12、`Content-Language`;任一接口都可作签名/时效负例。
- **转发**:sgs 只做接入(验签/限流/配置),业务在 [[svc_acquireii]];定位问题先分清"卡在网关(sgs 日志有 Receive/Sign 但无下游)"还是"到了收单核心"。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[auto_online_business_direct_pay]](自动化:直连支付自动化)
- [[flow_botim_wallet_binding_auth]](流程:BOTIM 钱包绑定/登录/Token 刷新认证流程)
- [[flow_zand_fundout]](流程:ZAND渠道出款端到端流程(SP/SQ/VS))
- [[scn_offline_merchant_scan_payment_code]](场景:商户扫用户付款码线下收单(POS / 扫码枪))
- [[scn_online_business_direct_pay]](场景:直连支付 (Direct Pay))
- [[scn_online_business_merchant_async_notify]](场景:商户异步通知接收与重试 (Open API))
- [[scn_online_business_mpgs_channel]](场景:MPGS 渠道卡支付(3DS2 / MOTO / 设备支付 / 卡组织拆分 / 退款Void))
- [[scn_online_business_openapi_protocol_signing]](场景:商户 Open API 接入协议与签名/加密规则)
- [[scn_online_business_payment_code_scan]](场景:付款码被扫线下收单 (POS / 扫码枪))
- [[scn_payment_core_mit_cit_mpgs]](场景:MIT/CIT MPGS 循环（tokenized）支付测试)

## 来源与置信
- UAT Kibana 实测(`java-kafka-logstash-*`,2026-07-03):app_id=`sgs` 近7d 773490 docs;Top mClass 为 ReceiveOrderService/SignService/Acs*(限流/密钥/商户配置/语言);运行于 `http-nio-8080`,包 `com.uaepay.gateway.sgs`,Zookeeper/Dubbo 注册。
- 下游 acquireii 为架构确定边(网关 Dubbo 转发,`*ClientImpl` 调用图采不到)。app_group=`gp028` · domain=`online-business`。
