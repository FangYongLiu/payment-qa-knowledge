---
id: scn_botim_payby_integration
object_type: Scenario
name: Botim-PayBy 服务端集成(gRPC 网关 / 加解密 / Bind Customer / UID 兼容 / Outbound API)
aliases: [Botim集成, Botim-PayBy gRPC, bind-customer, Botim UID兼容]
domain: channel
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/1072791687; confluence:PMDPayment/1184563231; wiki:a01637cc-4974-45c3-b1e9-d194dac7ed1f
tags: [botim, payby, grpc, aes-gcm, bind-customer, uid, outbound-api, 集成]
related_services: []
related_tables: []
related_logs: []
---

# Botim-PayBy 服务端集成

## 触发 / 入口
Botim 4.0 与 PayBy 服务端集成的测试与排障参考:gRPC 网关协议、报文 AES-GCM 加解密、Bind Customer 场景判定、UID/手机号变更兼容、PayBy↔Botim Outbound API 清单。登录/刷新时序见 [[flow_botim_payby_login]]。
集成目标:实现 gRPC 网关 + 客户信息交换 + 服务端登录与刷新 Token + 兼容既有 PayBy↔Botim API。
注:api_personal_bind_customer / api_personal_login_or_refresh / api_personal_v3_auth_login 等接口对象,以及 personal/member 服务对象,域内尚未建,正文用纯文字 + 标待补。

## 关联关系
- **涉及服务**:botim、personal、member、sgs/sgs-grpc、pts、cps(服务对象待补)
- **登录/刷新流程**:[[flow_botim_payby_login]]

## gRPC 网关协议(at_df / DownstreamCaller)
- proto:package `at_df`,service `DownstreamCaller`;`rpc send(DFRequest) returns Empty`(单向下行)、`rpc call(DFRequest) returns DFResponse`(请求/响应)。
- `DFRequest { bytes message = 1; }`;`DFResponse { bytes message = 1; DownstreamStatus status = 2; }`;`enum DownstreamStatus { OK=0; ERROR=1; }`。
- `message` 承载二进制编码(再经 AES-GCM 加密)的 `ApplicationMessage`。
- ApplicationMessage 顶层:`version`(byte)、`id`(Request ID,16)、`meta`(Meta)、`amp`(JSON payload)。
- Meta 字段:`adn`/`adm`/`asn`/`asm`(u8 长度前缀,≤127)、`amt`(u16,≤65535)、`amf`(2 bytes flags)、`amh`(Header map)、`ame`(u32 扩展)、`amc`(通信模式,默认 CALL)。
  - `adm` 指定调用的 API,如 `/personal/v1/bind-customer`。
  - Header 示例:`partner-id=20000000006`、`Content-Language=en/ar/zh`。
- 二进制编码:AMVer 1 字节;AMID 16 字节 UUID;ASN/ASM/ADN/ADM u8 长度+UTF-8;AMTrusty u16(big-endian);AMP u32(big-endian);AMFlag 2 字节;AMHeaders u8 数量 + N×(key u8len+value u16len)。
  - 解码错误:AMVer/AMID too short、String length missing/incomplete、Invalid UTF-8、AMP length/payload incomplete、AMFlag too short。

## 报文加解密(AES-256/GCM/NoPadding)
- 算法 `AES/GCM/NoPadding`;密钥 AES-256;`GCM_NONCE_LENGTH=12`、`GCM_TAG_LENGTH=16`。
- 加密产物布局:`12 bytes nonce || ciphertext(含 16B GCM tag)`,整体 Base64 编码。
- 加密:SecureRandom 生成 12B nonce → `GCMParameterSpec(GCM_TAG_LENGTH*8, nonce)` 初始化 ENCRYPT → doFinal → 写 `nonce||ciphertext` → Base64。
- 解密:Base64 解码 → 校验长度 `>= GCM_NONCE_LENGTH + GCM_TAG_LENGTH`(否则 `Invalid encrypted data length`)→ 切前 12B nonce → DECRYPT doFinal。
- 明文为 JSON(UTF-8),即 `ApplicationMessage.amp`,如 `{"requestTime":...,"bizContent":{"mobileNumber":"xxxx","uid":"xxx"}}`。
- 测试参考:`BotimGrpcServiceImplTest#testDecryptReplace_success`;敏感数据(如 mobile number)在 cgs→personal 时需加密。

## Bind Customer 场景判定(/personal/v1/bind-customer)
按 Mobile Number + UID + Old UID 匹配关系决定行为:
| 场景 | 处理 |
|---|---|
| 同手机号、UID 已存在 | idempotent,返回已存在 member |
| 手机号在 PayBy 不存在 | Create member(开通 AED BASIC,签 basic account 协议 + TOU) |
| 手机号已存在 member 但未关联 Botim UID | Bind with exist member |
| 手机号已存在 Botim UID 且与 Old UID 相同(仅 3.0→4.0) | Replace Botim UID |
| 手机号已存在 Botim UID 且与 Old UID 不同 | 不允许任何操作 |
- 入参:Mobile Number-M、Botim UID-M、Client IP-M、Botim Old UID-O;返回 Member ID-M。
- Replace UID 入参:Member ID-M、Old Botim UID-M、New Botim UID-M。
- 新建 member 需签协议:`USER_PRIVACY`、`BASIC_ACCOUNT`(`protocolService.queryAndSignProtocol`);member api `IMemberFacade#createMemberBotimFour`。

## UID / 手机号变更兼容
- Botim 4.0.0/4.0.1 UID 与 3.0 兼容;4.0.2 客户端改用 **AUID** 统一 PayBy/Botim/Quantix 登录,因此仍需 bind-customer(老用户 Replace UID,新用户 Create/Bind UID)。
- 4.0.2 Bind 动作:解除 3.0 UID 关联 → 关联 4.0 UID →(首次进 4.0 钱包)签 basic account 协议 + TOU。
- 关键决策:Botim 换手机但 PayBy 仍持旧号 → 保持现状(后续讨论);手机号已存在系统 → 更新 member UID 无需校验(Yun);不允许回退 Botim 3.0(Long)。
- 待处理场景:Botim/PayBy 换手机、PayBy 换手机→新手机已存在 member 被替换成 null、Botim/PayBy 注销后重注册。
- 已知问题:sgs 网络互通(涉加解密)、好友转账 3.0→4.0 无法领取、升级后数据前后不一致。

## PayBy ↔ Botim Outbound API(节选)
| API | 用途 | 场景/调用方 |
|---|---|---|
| `/api/uaepay/payby/callback/getUserInfo` | UID 查用户信息 | 好友转账、AA Split、CMS、自动注册;member/socialpay/basis-cms/personal |
| `/api/cuserrs/user/v1/userInfoDetail` | Auth Code 查用户信息 | personal |
| `/api/buserrs/user/v1/inner/batchGetUidByMobile` | 手机号反查 UID | household、basis-cms |
| `/api/uaepay/payby/callback/isGiftMember` | 官方 Cash Gift 群校验 | socialpay redpkg/receive |
| `/api/uaepay/payby/callback/isGroupMember` | 群成员校验 | Cash Gift 领取 |
| `/api/authserver/oauth2/token` / `/personal/auth/oauthByAuthCode` / `/personal/auth/loginByAuthCode` | OAuth / 登录 | personal 等 |
| `/api/officialrs/msg/v1/sendShoppingCartCardMsg` 等 | Household 卡片消息 | household |
| `/api/buserrs/lpage/upsertTodo` / `closeTodo` | Landing Page Todo 卡片 | cns、remittance |
| `https://uaepaygw.botim.me/api/uaepay/payby/callback/notify` | 通用通知触达 | Friend Transfer/Cash Gift/Aani;socialpay/personal/ons |
- 4.0 兼容:3.0 才有的通知(好友转账/Cash Gift/Household/Landing Page/Status Tracker)由 Botim 侧兼容;收款方未注册 PayBy 时经 getUserInfo 反查手机号,Botim 兼容。

## 协议选型
- GRPC 候选;SGS(HTTP)通过 SGS 提供 HTTP 服务并合并 bind-customer 与 refresh token(待评估)。
- Revision:2025-04-02 首版(Zhibin);2025-06-23 改用 sgs http protocol、合并 authToken 与 login(Huihua);2025-09-04 调整 UID 兼容(Huihua)。

## DB / 校验点
- bind-customer 各分支落库:member 创建/绑定/UID 替换是否符合矩阵。
- 加解密往返:密文长度、nonce 切分、UTF-8 解码、GCM tag 校验。
- 登录/刷新 token 链路与失败重登录。
> api 接口对象、服务对象待补;不确定项标待补。
