---
title: Botim-PayBy服务端集成时序流程
domain: payby-open-api
kind: wiki_page
slug: botim-payby-server-integration-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:d34203e7-c1b5-4464-b9ba-5424888fdab2
tags: []
---

# Botim-PayBy服务端集成时序流程

本页描述 Botim 绑定 PayBy 钱包的服务端时序，覆盖首次签约绑定客户（First Authentication）以及后续登录/刷新 token 的调用流程。

## 参与方（Lifelines）

按调用顺序从左到右：

- `user`（actor）
- `botim`
- `sgs-grpc`
- `personal`
- `pts`
- `member`
- `protocol`

`botim` 作为客户端网关调用 `sgs-grpc`，由 `sgs-grpc` 再委托至下游服务（`personal`、`pts`、`member`、`protocol`）。

## 入口流程

1. **Use Wallet**：user 在 botim 上发起使用钱包动作。
2. **Check bind PayBy or not**：user → botim 检查是否已绑定 PayBy。
   - 2.1 botim → user 返回结果。

## 首次签约（First Authentication）

仅在尚未绑定 PayBy 时执行，用于注册/更新客户并完成协议签署。

- 3. **Show PayBy protocol page**：botim 自身动作，展示 PayBy 协议页。
- 4. **Login and sign protocol**：user → botim 登录并签署协议。
- 4.1 **`/personal/v1/bind-customer`**：botim → sgs-grpc。
  - 4.1.1 **Bind customer**：sgs-grpc → personal。
    - 4.1.1.1 **Register or update customer**：personal → member。
    - 4.1.1.2 返回：member → personal。
    - 4.1.1.3 **Sign protocols**：personal → protocol。
    - 4.1.1.4 返回：protocol → personal。
  - 4.1.2 返回：personal → sgs-grpc。
- 4.2 **Member ID**：sgs-grpc → botim 返回会员标识。

## 登录 / 刷新 Token 流程

首次签约完成之后（或后续每次需要 token 时）执行。

- 4.3 **`/personal/v1/login-or-refresh`**：botim → sgs-grpc。
  - 4.3.1 **Login**：sgs-grpc → personal。
    - 4.3.1.1 **Apple token**：personal → pts。
    - 4.3.1.2 **Access token**：pts → personal。
  - 4.3.2 **Access token**：personal → sgs-grpc。
- 4.4 **Access token**：sgs-grpc → botim。
- 4.5 **Save token or anything**：botim 自身动作，保存 token 等信息。
- 4.6 **Botim token**：botim → user 下发 botim 侧 token。

## 关键接口一览

| 接口路径 | 调用方向 | 用途 |
|---|---|---|
| `/personal/v1/bind-customer` | botim → sgs-grpc | 首次签约：绑定客户、签署协议 |
| `/personal/v1/login-or-refresh` | botim → sgs-grpc | 登录或刷新，换取 Access token |

## 关键返回值

- **Member ID**：由 `bind-customer` 流程在 sgs-grpc 返回给 botim。
- **Access token**：由 `login-or-refresh` 流程经 pts → personal → sgs-grpc → botim 透传。
- **Apple token**：personal 向 pts 提交以换取 Access token 的中间凭证。
