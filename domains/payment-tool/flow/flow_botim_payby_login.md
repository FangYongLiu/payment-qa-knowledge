---
id: flow_botim_payby_login
object_type: Flow
name: Botim-PayBy 服务端登录与 Token 刷新流程
aliases: [Botim登录, Botim token refresh, personal v3 auth login]
domain: payment-tool
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/1072791687; wiki_image:80e249f0-da50-4572-b397-a7d1c4b13711; wiki_image:e6841f36-24d4-4fcc-9708-5a7164389d09; wiki_image:a568cec9-2bcf-4a35-b6cd-0a493e9f90e1
tags: [botim, payby, login, token-refresh, grpc, personal]
related_services: []
related_tables: []
related_scenarios: [scn_botim_payby_integration]
---

# Botim-PayBy 服务端登录与 Token 刷新流程

## 概述
Botim 4.0 与 PayBy 服务端集成的登录与 Token 刷新链路:Botim App 先在 Botim 自有服务完成认证,再经 sgs 网关(gRPC)进入 personal 服务,由 personal 编排设备落库、静默登录与风控咨询,最终把 accessToken 返回客户端。Token 刷新由 pts 实际颁发,经 personal → sgs → botim 逐层回传;刷新失败走重登录。
注:涉及 api_personal_* 接口对象与 personal/member/pts/cps 服务对象,域内尚未建,正文用纯文字 + 标待补。

## 步骤(跨系统)
### 登录流程(/personal/v3/auth/login)
1. app use → botim app:`login`。
2. botim app → botim server:`botim login`(botim server 自校验 `verified`)。
3. botim app → botim server:`payby login`。
4. botim server → sgs:`/personal/v3/auth/login`。
5. sgs → personal:`with device info`(携带设备信息)。
6. personal 内部编排:
   - `checkAvailable`(自检);
   - `IDefaultDeviceFacade#save`(→ pts 保存设备);
   - `AccessTokenFacade#silentLogin`(→ member 静默登录);
   - `ConsultRiskServiceStub#consultRiskManager`(→ cps 风控咨询);
   - 返回 `accessToken` → sgs → botim server → botim app。

### Token 刷新流程(/personal/v1/refresh-token)
1. user → botim:`Refresh token`。
2. botim → sgs-grpc → personal → pts:逐层转发刷新。
3. pts 生成 `New token` → personal → sgs-grpc → botim(逐层回传)。
4. botim `Save token`(仅拿到有效 New token 时保存)→ 响应 user。
5. **刷新失败分支**:botim 判定失败 → 触发 `Re-login` 走重登录,不继续使用旧/新 token。

### gRPC 请求内部处理时序(Botim 4.0.1)
- `BotimGrpcServiceImpl`(入口):check param → deserialize ApplicationMessage → processRequest。
- `ReceiveOrderService`(编排):check api config → doService(→ AppService 业务逻辑)→ get service response → encrypt response → transformResponse → write grpc response(→ WriteResponseAssist)。

## 关联关系
- **经过的服务(有序)**:botim app → botim server → sgs → personal →(pts / member / cps);刷新 botim → sgs-grpc → personal → pts(服务对象待补)
- **关键场景 / 参考**:[[scn_botim_payby_integration]](网关协议、加解密、bind-customer、outbound API)

## 校验点
- Botim 侧认证(botim login/verified)与 PayBy 侧登录(payby login)是两段独立但顺序衔接的流程。
- PayBy 登录入口固定网关路径 `/personal/v3/auth/login`(合并原 `/personal/apply/authToken` 与 `/personal/v2/auth/login`),由 sgs 透传至 personal。
- token 生成职责归 pts;sgs/sgs-grpc 仅中转;botim 负责本地校验与持久化。
- 刷新失败必须走重登录;仅在拿到有效 New token 时执行 Save token。
- personal 是登录编排中枢,协同 pts(设备)、member(令牌)、cps(风控)三方。
