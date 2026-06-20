---
title: H5 jsBridge认证流程
domain: payby-core-systems
kind: wiki_page
slug: h5-jsbridge-auth-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:b65e63bb-0d70-489b-b879-6ef5b8824393
tags: []
---

# H5 jsBridge认证流程

H5 页面通过 jsBridge 向 Native App 请求 challenge，由 http gateway 转发到 cgs-grpc 生成 verifier token，再经 cgs-http 验证后建立 session。

## 参与方

- user
- h5 page
- native app
- http gateway
- cgs-grpc
- cgs-http

## 时序步骤

1. **Open H5 page**：user → h5 page，用户打开 H5 页面。
2. **Request jsBridge H5 challenge**：h5 page → native app，H5 页面通过 jsBridge 向 Native App 请求 challenge。
   1. **/h5app/auth/apply**：native app → http gateway，Native App 调用 http gateway 的申请接口。
      1. **gRPC call**：http gateway → cgs-grpc，gateway 通过 gRPC 转发到 cgs-grpc。
         1. **Generate H5 verifier token**：cgs-grpc 内部生成 H5 verifier token。
         2. 返回 token 给 http gateway（dashed）。
      2. http gateway 返回给 native app（dashed）。
   2. **Verifier token**：native app → h5 page（dashed），将 verifier token 返回 H5 页面。
3. **/h5app/auth/v2/verify**：user → cgs-http，由 user 侧直接调用 cgs-http 的验证接口。
   1. **Verify token & set up session**：cgs-http 内部校验 token 并建立 session。
   2. **Session id**：cgs-http → user（dashed），返回 session id。

## 接口

- `/h5app/auth/apply`：申请 H5 verifier token，由 native app 调用 http gateway。
- `/h5app/auth/v2/verify`：校验 verifier token 并建立 session，由 cgs-http 提供。

## 备注

- 实线箭头表示请求，虚线箭头表示响应。
- verifier token 的生成位于 cgs-grpc，session 的建立位于 cgs-http。
