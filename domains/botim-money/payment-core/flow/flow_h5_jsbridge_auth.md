---
id: flow_h5_jsbridge_auth
object_type: Flow
name: H5 客户端 jsBridge 鉴权流程(Verifier Token + Session)
aliases:
- h5-jsbridge-auth
- h5-client-auth
- H5鉴权
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: wiki_image:97ce143e-fc5c-4cc6-a2ab-f036cb1a996b; wiki_image:b65e63bb-0d70-489b-b879-6ef5b8824393
tags:
- h5
- auth
- jsbridge
- cgs
- session
related_services:
- svc_cgs
related_tables: []
related_scenarios: []
---

# H5 客户端 jsBridge 鉴权流程(Verifier Token + Session)

## 概述
H5 页面通过 native app 桥接申请 verifier token,再由 H5 页面直接向 cgs-http 校验并建立会话的两阶段鉴权流程。其中 cgs-grpc 与 cgs-http 均为 [[svc_cgs]] 的接入形态(分别承担 token 生成与 session 建立),http gateway / native app / h5 page 为客户端侧外部参与方。

## 步骤(跨系统)

### 阶段一:申请 Verifier Token(经 native app + gateway + gRPC)
1. user → h5 page:打开 H5 页面。
2. h5 page → native app:通过 jsBridge 请求 H5 challenge。
3. native app → http gateway:`/h5app/auth/apply`。
4. http gateway → cgs-grpc([[svc_cgs]]):gRPC call。
5. cgs-grpc 内部生成 H5 verifier token。
6. 沿原路径返回:cgs-grpc → http gateway → native app。
7. native app → h5 page:回传 verifier token。

### 阶段二:校验 Token 并建立会话(H5 直连 cgs-http)
8. h5 page / user → cgs-http([[svc_cgs]]):`/h5app/auth/v2/verify`,提交 verifier token。
9. cgs-http 校验 token 并建立 session。
10. cgs-http → h5 page / user:返回校验结果 / session id。

## 关联关系
- **经过的服务(有序)**:http gateway(外部) → [[svc_cgs]](cgs-grpc 生成 token → cgs-http 校验并建会话)(= `related_services`)
- **外部参与方**:user、h5 page、native app、http gateway
- **关键表**:待补
- **关键场景**:待补

## 关键接口
- `/h5app/auth/apply`:申请 H5 verifier token(native app 调 http gateway,转 cgs-grpc 生成)。
- `/h5app/auth/v2/verify`:校验 verifier token 并建立 session(cgs-http 提供)。

## 校验点
- 两阶段职责分离:token 由 cgs-grpc 生成,session 由 cgs-http 建立。
- H5 页面无法直接申请 token,必须通过 native app 的 jsBridge 桥接;校验阶段 H5 直连 cgs-http(跳过 native app 与 gateway)。
- 实线表请求、虚线表响应。
