---
title: Botim 4.0.1 接入细节与调优清单
domain: channel-integration
kind: wiki_page
slug: botim-4-0-1-integration-details
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:2760a835-37a3-4c85-8a82-bd47dd28a5ca
tags: []
---

# Botim 4.0.1 接入细节与调优清单

本页梳理 Botim 4.0.1 接入过程中的协议通道选型、`/bind-customer` 接口的调优要点、敏感数据加密以及新建会员时需签署的协议清单。

## 协议通道选型

- **GRPC**：作为 Botim 4.0.1 接入的可选通道之一。
- **SGS (HTTP)**：使用 SGS 提供 HTTP 服务，并考虑将 `bind-customer` 与 refresh token 接口合并对外提供。

## /bind-customer 调优要点

- 对**已存在的 member**，使用 member api 进行绑定或替换 uid。
- 调用接口：
  - interface：`com.uaepay.member.service.facade.IMemberFacade#createMemberBotimFour`
  - version：`1.0.53-SNAPSHOT`

## 敏感数据加密

- 在 cgs 向 personal 发送数据时，对敏感数据（如 mobile number）启用加密。
- 参考测试用例：`com.uaepay.gateway.sgs.auto.ext.service.botimgrpc.BotimGrpcServiceImplTest#testDecryptReplace_success`

## 新建会员协议签署

新建会员时需签署的协议（参考 personal service 中的 member creation 流程）：

- `USER_PRIVACY`
- `BASIC_ACCOUNT`

代码参考：`protocolService.queryAndSignProtocol`
