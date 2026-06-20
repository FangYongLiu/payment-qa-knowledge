---
id: api_personal_bind_customer
object_type: API
domain: channel-integration
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:a01637cc-4974-45c3-b1e9-d194dac7ed1f
tags:
- personal
- bind
- uid
- member
subdomain: personal
module: sgs-api
sensitivity: normal
name: 绑定客户接口
aliases:
- Bind Customer
- /personal/v1/bind-customer
related_services: []
related_tables: []
related_scenarios:
- botim-uid-compatibility-cases
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
- 在 Botim 客户首次使用 4.0 钱包功能时，由 Botim 调用 PayBy 完成 Botim UID 与 PayBy member 的关联。
- 支持三种动作：
  - Create member：手机号在 PayBy 不存在时新建 member，激活 AED BASIC 账户，签署 basic account protocol 与 TOU。
  - Bind with exist member：手机号已存在 PayBy member 但未关联 Botim UID 时，把 4.0 Botim UID 关联到该 member，签署 basic account protocol 与 TOU。
  - Replace Botim UID（3.0 升级 4.0）：解除 3.0 Botim UID 的关联，将 4.0 Botim UID 关联到该 member。
- Botim 4.0.2 起客户端使用 AUID，本接口用于为老用户更新 UID、为 4.0.2 新用户创建 UID。

## 路径/方法
- API Code：`/personal/v1/bind-customer`
- API Name：Bind Customer
- 调用方式：通过 gRPC 网关 `DownstreamCaller.call(DFRequest) returns (DFResponse)` 承载，`ApplicationMessage.meta.adm = /personal/v1/bind-customer`。
- 文档入口：http://sim.intra.test2pay.com/api-doc/sgs-api/personal-sgs-api/

## 入参
Application Message → Meta → adh（Header）：
- `partner-id`：Partner ID（示例 `20000000006`）
- `Content-Language`：`en` / `ar` / `zh`

Application Message → amp（JSON 业务报文，整体走 AES-256/GCM/NoPadding 加密，Base64 传输；amp 示例结构）：
```
{
  "requestTime": 17691238142134,
  "bizContent": {
    "mobileNumber": "xxxx",
    "uid": "xxx"
  }
}
```

bizContent 字段（M=必填，O=可选）：
- `mobileNumber` - M：客户手机号
- `uid` - M：Botim UID（用于建立与 Botim 的关系）
- `clientIp` - M：Client IP
- `oldUid` - O：Botim Old UID（可为 3.0 UID）

## 出参
- `memberId` - M：PayBy Member ID

按手机号绑定的处理矩阵：
| 场景 | 行为 |
| --- | --- |
| Same Mobile、UID existed | 幂等，返回已存在的 member |
| Mobile not exist PayBy member | Create member |
| Mobile exist PayBy member but no Botim UID associated | Bind with exist member |
| Mobile exist Botim UID 且与 Botim Old UID 一致（仅 3.0 → 4.0） | Replace Botim UID（botim3.0 / botim4.0 UID 相同情况） |
| Mobile exist Botim UID 且与 Botim Old UID 不一致 | Not allow to do anything |

personal 内部能力：
- Replace UID 入参：`memberId` - M、`oldUid` - M、`newUid` - M
- Bind UID to Member 入参：`memberId` - M、`uid` - M

## 错误码
原文未列出本接口的具体错误码（详见 Personal Documentation：sgs-api/personal-sgs-api）。

## 测试校验点
- 协议页展示：仅在客户首次使用 4.0 钱包时展示。
- 必填校验：`mobileNumber`、`uid`、`clientIp` 缺失需拒绝；`oldUid` 可空。
- Header 校验：`partner-id`、`Content-Language` 必须随请求传入。
- 加解密：amp 必须使用 AES-256、AES/GCM/NoPadding、12 字节 nonce 前置 + 密文，Base64 编码后传输；解密失败应返回错误。
- 场景矩阵覆盖：
  - 同 Mobile + 同 UID：返回已存在 member（幂等，不重复创建）。
  - 新 Mobile：创建 member，激活 AED BASIC 账户，签署 basic account protocol 与 TOU。
  - Mobile 存在但无 UID：仅做绑定，签署 protocol 与 TOU。
  - Mobile 存在 UID 且 == oldUid（3.0→4.0）：解绑旧 UID，绑定新 UID（Replace）。
  - Mobile 存在 UID 且 != oldUid：拒绝任何操作。
- 4.0.2 兼容：AUID 场景下，老用户走 UID 更新分支，新用户走 UID 创建分支。
- 与登录接口联动：绑定成功后，可由 `/personal/v1/login-or-refresh` / `/personal/v3/auth/login` 用 `memberId` + `uid` 换取 Access Token。
- 手机号变更类用例（参见 botim-uid-compatibility-cases）：Botim 换手机、PayBy 换手机、PayBy 换手机后新手机已有 member 被替换为 null、Botim/PayBy 注销重注册等流程下 bind-customer 行为符合矩阵。
