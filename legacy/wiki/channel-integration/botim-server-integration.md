---
title: BOTIM服务端集成说明
domain: channel-integration
kind: wiki_page
slug: botim-server-integration
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:a5832e48-f1cb-4a92-9081-b0203e7859dc
tags: []
---

# BOTIM服务端集成说明

本页描述 BOTIM 在服务端集成场景下，与 `sgs-grpc`、`pts` 之间完成 token 校验与刷新的时序流程。

## 参与方

- **user**：业务调用发起方
- **botim**：BOTIM 服务端
- **sgs-grpc**：中转服务（对接 pts）
- **pts**：token 生成方

## Token 刷新时序

整体流程由用户在 botim 上触发业务动作开始，由 botim 完成本地 token 校验，必要时经 sgs-grpc 向 pts 申请新 token，最终回写并响应用户。

具体步骤如下：

1. **Do something**：user → botim，发起业务请求。
   1. **Check token**：botim 本地自检 token。
   2. **Refresh token**：botim → sgs-grpc，请求刷新。
      1. **Refresh token**：sgs-grpc → pts，转发刷新请求。
         1. **Generate new token**：pts 在本地生成新 token（pts 上有 activation 激活区间）。
         2. 返回：pts → sgs-grpc（虚线返回）。
      2. **New token**：sgs-grpc → botim，返回新 token（虚线返回）。
   3. **Save token**：botim 本地保存新 token。
   4. 返回：botim → user（虚线返回），完成业务响应。

## 调用语义说明

- 实线箭头表示同步调用。
- 虚线箭头表示返回（response）。
- token 的生成职责归属 **pts**；sgs-grpc 仅做中转；botim 负责本地校验与持久化保存。
