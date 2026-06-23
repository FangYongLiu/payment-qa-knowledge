---
title: Botim 4.0.1 接入细节与调优清单
domain: channel-integration
kind: wiki_page
slug: botim-4-0-1-integration-details
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/1184563231
tags: []
---

# Botim 4.0.1 接入细节与调优清单

本页汇总 Botim 4.0.1 接入过程中协议选型、绑定改造、敏感数据加密以及新建会员协议签署等待办事项与技术要点。

## 协议选型（Protocol Selection）

- **GRPC**：候选方案之一。
- **SGS (HTTP)**：通过 SGS 提供 HTTP 服务，并合并 `bind-customer` 与 refresh token 接口（待评估）。

## 调优 TODO

### /bind-customer 改造

对已存在的 member，使用 member api 进行绑定或替换 uid：

- 接口：`com.uaepay.member.service.facade.IMemberFacade#createMemberBotimFour`
- 版本：`1.0.53-SNAPSHOT`

### 敏感数据加密

- 当 cgs 向 personal 发送数据时，需对敏感数据（如 mobile number）启用加密。
- 测试参考：`com.uaepay.gateway.sgs.auto.ext.service.botimgrpc.BotimGrpcServiceImplTest#testDecryptReplace_success`

### 新建会员协议签署

新建 member 时需签署的协议（参考 personal 服务中的会员创建逻辑）：

- `USER_PRIVACY`
- `BASIC_ACCOUNT`

代码参考：`protocolService.queryAndSignProtocol`
