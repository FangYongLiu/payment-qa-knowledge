---
title: H5客户端鉴权流程(jsBridge + Verifier Token)
domain: payby-core-systems
kind: wiki_page
slug: h5-client-auth-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:97ce143e-fc5c-4cc6-a2ab-f036cb1a996b
tags: []
---

# H5客户端鉴权流程(jsBridge + Verifier Token)

H5 页面通过 native app 桥接申请 verifier token，再由 H5 页面直接向 cgs-http 校验并建立会话的两阶段鉴权流程。

## 参与方

- user：用户
- h5 page：H5 页面
- native app：原生 App 容器
- http gateway：HTTP 网关
- cgs-grpc：核心鉴权 gRPC 服务
- cgs-http：核心鉴权 HTTP 服务（负责会话建立）

## 阶段一：申请 Verifier Token

通过 jsBridge 由 native app 代为向后端申请 token。

1. user → h5 page：打开 H5 页面
2. h5 page → native app：通过 jsBridge 请求 H5 challenge
3. native app → http gateway：调用 `/h5app/auth/apply`
4. http gateway → cgs-grpc：发起 gRPC 调用
5. cgs-grpc：内部生成 H5 verifier token
6. 沿原路径返回：cgs-grpc → http gateway → native app
7. native app → h5 page：回传 verifier token

## 阶段二：校验 Token 并建立会话

H5 页面直接与 cgs-http 通信，跳过 native app 与 gateway。

1. h5 page → cgs-http：调用 `/h5app/auth/v2/verify`，提交 verifier token
2. cgs-http：校验 token 并建立 session
3. cgs-http → h5 page：返回校验结果

## 关键点

- 两阶段设计：申请阶段经 native app + gateway + gRPC，校验阶段 H5 直连 cgs-http。
- Token 由 cgs-grpc 生成，由 cgs-http 校验，职责分离。
- H5 页面无法直接申请 token，必须通过 native app 的 jsBridge 桥接。
