---
id: flow_botim_wallet_binding_auth
object_type: Flow
name: BOTIM 钱包绑定/登录/Token 刷新认证流程
aliases:
- botim-wallet-binding-auth
- botim-payby-auth
- botim-token-refresh
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: wiki_image:00ee9166-336e-44bf-9e4b-e170fd8e95cb; wiki_image:5b1644df-997f-479d-8160-f0b57c5a9f5b; wiki_image:0eb622de-7e30-4c72-9fce-f6ecec6f59d6
tags:
- botim
- auth
- 绑定
- token
- sgs-grpc
related_services:
- svc_sgs
- svc_personal
- svc_pts
- svc_member
- svc_protocol
related_tables: []
related_scenarios: []
---

# BOTIM 钱包绑定/登录/Token 刷新认证流程

## 概述
用户在 BOTIM 中使用 PayBy 钱包时的端到端认证链路:BOTIM 作为客户端网关,统一通过 `sgs-grpc`([[svc_sgs]] 的 gRPC 接入层)调用 PayBy 后端;sgs-grpc 向下委派 [[svc_personal]],personal 协调 [[svc_member]](注册/更新)、[[svc_protocol]](协议签署)、[[svc_pts]](Token 颁发)完成首次绑定、登录与 Token 下发,并支持 Token 刷新与失败重登录。

> 首次流程产出两类关键标识:**Member ID**(绑定阶段)与 **Access token**(登录阶段),最终由 botim 转换为 **Botim token** 下发给 user。

## 步骤(跨系统)

### A. 入口:检测绑定状态
1. Use Wallet:user 在 botim 触发使用钱包。
2. Check bind PayBy or not:user → botim,检查是否已绑定 PayBy → 返回结果。

### B. First Authentication(首次认证:绑定客户 + 签署协议)
3. Show PayBy protocol page:展示协议页。
4. Login and sign protocol:user → botim,登录并签署协议。
   - 4.1 `/personal/v1/bind-customer`:botim → sgs-grpc([[svc_sgs]])
     - 4.1.1 Bind customer:sgs-grpc → [[svc_personal]]
       - 4.1.1.1 Register or update customer:personal → [[svc_member]]
       - 4.1.1.2 member → personal(返回)
       - 4.1.1.3 Sign protocols:personal → [[svc_protocol]]
       - 4.1.1.4 protocol → personal(返回)
     - 4.1.2 personal → sgs-grpc(返回)
   - 4.2 Member ID:sgs-grpc → botim

### C. 登录与 Token 下发
   - 4.3 `/personal/v1/login`(或 `/personal/v1/login-or-refresh`):botim → sgs-grpc
     - 4.3.1 Login:sgs-grpc → [[svc_personal]]
       - 4.3.1.1 Apply token:personal → [[svc_pts]]
       - 4.3.1.2 Access token:pts → personal
     - 4.3.2 Access token:personal → sgs-grpc
   - 4.4 Access token:sgs-grpc → botim
   - 4.5 Save token or anything:botim 本地保存
   - 4.6 Botim token:botim → user

### D. Token 刷新(Refresh)
1. user → botim:Refresh token
2. botim → sgs-grpc:`/personal/v1/refresh-token`
3. sgs-grpc → [[svc_personal]]:Refresh token
4. personal → [[svc_pts]]:Refresh token → 返回
5. 逐层返回 personal → sgs-grpc → botim
- **失败处理(Refresh Failed)**:refresh-token 失败时,botim 执行 Re-login(重新走 B/C 流程获取新 Token)。
- botim 执行 Save token,并向 user 返回 Response。

## 关联关系
- **经过的服务(有序)**:botim(外部客户端网关) → [[svc_sgs]](sgs-grpc) → [[svc_personal]] →([[svc_member]] / [[svc_protocol]] / [[svc_pts]])(= `related_services`)
- **关键表**:待补
- **关键场景**:待补

## 关键接口
- `/personal/v1/bind-customer`:绑定客户(注册/更新会员 + 签署协议)
- `/personal/v1/login` / `/personal/v1/login-or-refresh`:登录或刷新,换取 Access token
- `/personal/v1/refresh-token`:刷新 Token

## 校验点
- 首次绑定必须先完成 member 注册/更新与 protocol 协议签署,才返回 Member ID。
- 登录由 pts 颁发 Access token,经 personal → sgs-grpc 透传至 botim,再转为 Botim token。
- Token 刷新失败必须触发 Re-login 兜底,保证会话不中断。
