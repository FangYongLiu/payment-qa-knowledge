# 业务域划分 · 确认记录 + 剩余待确认

> 临时工作文档。三方交叉(现有库 / Confluence 官方 / Botim Money Tech Team 频道)后已确认大部分;
> 剩余"需 dev-lead"的一小撮见 §3。定稿后据此重整 `domains/` 并删除本文件。

## 1. 已确认的决策

**业务域**
- **A1 Lending**:原 `quantix` 里的 `botim-snpl / paylater / botim-credit / credit-business / cbm / cqm` = 借贷/BNPL(SME Lending 团队)→ 域改名 **`lending`**。
- **A2 Crypto**:`cc-*` 全套(cc-trade/deposit/withdraw/channel-btc·eth·tron/ccdpm-*/cc-acquire/cc-cashier/holding/quotation)= 独立加密货币域 → 保留 **`crypto`**。
- **A3 Marketing**:coupon/promo/points 系列 = 独立域 → 保留 **`marketing`**。
- **A4 Atlas**:新平台**等上线再建**(现在不建骨架)。

**粒度(C)**
- **C1** PayCore **全拆**:payment-core / card / fundout / deposit-vam / channel / settlement / infrastructure。其中 **`channel` = Funds Channel**(专对接外部网关:MPGS/CKO/NPSS 等)。
- **C2** `fundout` 归 **payment-core 团队**;`merchant-fundout` 归 **商户团队**(→ merchant-management)。
- **C3** `notification`(pns)并入 **`infrastructure`**;`member` → **独立域**(见下方建议)。
- **C4** `kyc` 并入 **`compliance`**。
- **C5** `cs-portal` 并入 **`merchant-management`**(Chahid 技术团队)。

**channel 域 = Payment Tool 团队(PT,Jira key PT)**
- 负责人 **Kingo Liang**(kingo.liang@astratech.ae),成员 Hefei Zhang / Guoyou Ma。
- 职责:渠道订单生命周期(CMF)、路由(Router)、渠道适配器(MPGS/CKO/NI/Fiserv/AANI)、3DS、Fallback。
- 拥有服务:`cmf` `cmf-task` `fcw` `router` `qpay-cko` `qpay-nipos` `qpay-nisocket` `qpay-fsii`
  `qpay-fts`(CBUAE 资金转账)`cards`。
- ⚠️**更正**:`reconciliation`(渠道对账)、`counter`(结算管理后台)**不归 Kingo/PT,归 payment-core 团队**
  → 放 **`settlement`** 域,`dev_owner: payment-core`。

**两点我的建议(已采纳)**
- **member**:是全系统唯一身份实体,不应埋进 compliance(那是监管:KYC核验/AML/报送)→ **独立 `member`(会员/身份)域**。
- **counter/reconciliation**:按**能力**归 **`settlement`(清结算)**域(人/AI 找对账就来这);开发归属写进 frontmatter `dev_owner: payment-core`。
- **原则**:目录按**业务能力**分(便于查找),**开发团队归属放 `dev_owner` 字段**,两者解耦。
- **basis-***(运营审批后台,payment-core dev):按其管理的功能就近归位;`basis-merchant`→merchant-management,其余暂归 infrastructure/运营后台。

## 2. Kibana(UAT)探测到功能、已建议归属
| 服务 | 线索 | 建议域 |
|---|---|---|
| `rtp` | NpssClientImpl / ExpirePayerOrderJob | channel(实时支付) |
| `qpay-fts` | com.uaepay.channel.fts / SFTP / FtsQueryOrder | channel(文件对接) |
| `authpay` | SchemeServiceImpl / PayAuthorityFacade | payment-core |
| `csimple` | CardNotifyFacade | card |
| `pcbs` | DailyBalanceReport / CustomerLoad | settlement |
| `pts` | VerifyTokenFacade + Member/Kyc client | member(待确认) |
| `cbm` / `cqm` | 原 quantix | lending |
| `gadget` | CreateCaptchaProcessor | infrastructure |
| `basis-cms` | CMS/I18n 后台 | infrastructure(运营后台) |
| `host-gateway` | gateway | channel(待确认) |
| `user-profile-scheduler` | 用户档案定时 | member(待确认) |

## 3. 仍需 dev-lead 确认（这一小撮)

**日志里只有基础设施噪声、判不出功能:**
`tpay-nyu`(6800万条却全 Dubbo/ZK)、`tld-service`(NotifyOrderAutoAdvance,com.payby 新服务)、`adg`(DDS/PDF/PaymentScheduler)、`socialpay`、`pws`(含 Acs 类,疑风控?)、`custom`、`officer`、`leanlink`
- 各归哪个域?答:______

**UAT 无日志、只能靠命名(请确认):**
`exchange-rate-crawler`→FX? · `palm-id`→KYC(掌纹)? · `kiosk-mgmt`→offline? · `channel-paykii`/`channel-mobile-ding`→channel? · `youstore-installment`→lending? · `agreements-static`/`asite`/`afis`/`supplier`→?
- 答:______

**范围问题(重要):**
`life-center` / `market-goods` / `market-order` / `youstore` 看着像**生活服务/商城业务**——**是否属于本支付知识库的范围?** 还是另一条业务线不纳入?
- 答:______

## 4b. 服务归类(消化 service-catalog + payment-tools,不再保留未定义目录)

**按命名/探测归类(54 个):**
| → 域 | 服务 |
|---|---|
| payment-tool | cmf, cmf-task, fcw, router, qpay-fts, h2h, host-gateway, channel-paykii, channel-mobile-ding, rtp, exchange(DCC/FX) |
| payment-core | authpay, cashdesk-api, cashierii |
| card | csimple, gppc, gppc-jaywan |
| wallet | personal, transfer, deduct |
| settlement | pcbs, adg(PDF/statement,低置信) |
| member | pts, user-profile-scheduler |
| infrastructure | pns, gadget, cms, cmsii, basis-cms, custom, leanlink, asite, tld-service, tpay-nyu, exchange-rate-crawler |
| merchant-management | agreements-static, customer-service, supplier(低置信) |
| offline-business | kiosk-mgmt |
| lending | youstore-installment |
| compliance | palm-id, officer(低置信) |
| risk | afis(指纹?), pws(含 Acs,低置信) |
| online-business | socialpay(社交支付?低置信) |

**建议排除(非知识/非支付,不进库):**
- 测试 mock:`fundchannel-mock` `mock-channel` `mock-ni` `ni-mock` `mock-datawire` `pns-merchant-mocker`
- 疑非支付(生活/商城业务):`life-center` `market-goods` `market-order`

> 标"低置信"的老服务纯按命名判断;若 dev-lead 有异议可改。

## 4. 定稿域清单(草案见 `index/domains.draft.yaml`)
收单:online-business · offline-business · merchant-management
PayCore(拆):payment-core · card · fundout · deposit-vam · channel · settlement · infrastructure
独立:wallet · remittance · wps · risk · lending · crypto · marketing · member
跨切:compliance(含 kyc)  未来:atlas(暂不建)  元:service-catalog
