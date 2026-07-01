---
id: reference_jaywan_mbank_integration
object_type: Reference
name: Jaywan/mBank 卡集成参考(环境配置/密钥/对账结算/Chargeback/门户报表/产品矩阵)
aliases: [Jaywan mBank integration, gppc-OP env config, dgpay key exchange, jaywan reconciliation settlement]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/1143242758 + wiki_attachment:c35b0d12 + wiki_attachment:e3c2c891 + wiki:8bcc5af4 (gppc-OP 环境/密钥/对账结算/门户报表/产品矩阵)
tags: [jaywan, mbank, dgpay, env-config, key-exchange, reconciliation, settlement, chargeback, portal]
related_services: [svc_ppc]
---

# Jaywan/mBank 卡集成参考

> Jaywan 预付卡(MBank BIN Sponsor + Dgpays 处理方)机构对接的配置/运营/对账事实库。端到端业务流程见 [[flow_jaywan_prepaid_card]]。结算货币 AED、时区 UAE GST、对账 T+1(每日 04:00 AM GST 前交付)、每日结算。

## 1. 环境配置(gppc-OP / Dgpay)

### Dgpay 费用收单商户号(Jaywan Fee Collection)
| 环境 | 商户号 |
| --- | --- |
| SIM | 200000433440 |
| UAT | 200000083365 |
| PROD | 200024937979 |

### Dgpay Integration 网关 URL
- SIM/TEST:`https://testmbankprepaid.dgpays.com/NetaIntegrationGateway/api/AstraTechIntegrationService/{{METHOD_NAME}}`
- UAT:`https://kongapi.mbankuae-uat.local:8443/uat/api/AstraTechIntegrationService/{{METHOD_NAME}}`

### 产品号配置
| Item | SIM | UAT | PROD |
| --- | --- | --- | --- |
| ProductNumber | 051 | 051 | 051 |
| SubProductNumber | 051 | 051 | 051 |

### Institution API: gppc-jaywan(供 Dgpay 反向调用)
URL Prefix:
| 环境 | Prefix |
| --- | --- |
| SIM | `https://sim-gppc-ext.test2pay.com/gppc-jaywan/api/dgpay/{UrlSuffix}` |
| UAT | `https://uat-gppc-ext.test2pay.com/gppc-jaywan/api/dgpay/{UrlSuffix}` |
| PROD | `https://gppc-ext.payby.com/gppc-jaywan/api/dgpay/{UrlSuffix}` |

API 列表(UrlSuffix):`/get-token`、`/update-prepaid-card-status`、`/provision`、`/balance-inquiry`、`/reversal`、`/declined-transaction`、`/notify-courier-process`。

## 2. 密钥交换(PayBy ↔ DGPAY)

### 生成 PayBy RSA 公私钥(1408 bit)
```bash
openssl genrsa -out private.pem 1408
openssl rsa -in private.pem -pubout -out public.pem
openssl rsa -in private.pem -check
openssl pkcs8 -in private.pem -topk8 -nocrypt -out private_pkcs8.pem   # Java pkcs8
openssl rsa -pubin -in public.pem -text -noout -modulus               # 取 Modulus + Exponent 给 DGPAY
```
确认密钥位数(示例 1408 bit);Modulus 用于对端校验公钥一致性,需完整保留。

### Key Vault 存储路径
| Subject | Vault Type | Vault Key(SIM / UAT / PROD) |
| --- | --- | --- |
| PayBy Public Key | Certificate | `kv-biz-sim.payby-dgpay-rsa-publickey-01` / `kv-biz-uat.…` / `kv-biz-payby-prd.…` |
| PayBy Private Key | Secret | `kv-biz-sim.payby-dgpay-rsa-privatekey-01` / `kv-biz-uat.…` / `kv-biz-payby-prd.…` |
| DGPAY token password | Secret | `kv-biz-sim.3rddgpay-http-password-01` / …(username=`ASTRATECH`) |
| DGPAY publickey Modulus | Secret | `kv-biz-sim.3rddgpay-publickey-modulus-01` / … |
| DGPAY publickey Exponent | Secret | `kv-biz-sim.3rddgpay-publickey-exponent-01` / … |
| PayBy API token password | Secret | `kv-biz-sim.payby-dgpay-http-password-01` / …(username SIM=`sim-payby-dgpay`/UAT=`uat-payby-dgpay`) |

需提供给 DGPAY:PayBy 公钥 Modulus+Exponent、PayBy API Token username+password。DGPAY 联系人:`gokhan.leblebici@dgpays.com`。

## 3. 对账与结算(mBank,经 Dgpays)

### 对账文件
- 频率 T+1;送达 每日 04:00 AM GST 前;方式 SFTP;格式 Excel 或 CSV;覆盖窗口 前一日 00:00–23:59 GST;时区 UAE GST。
- 内容:Purchase / Refund / Declined / Chargebacks(如适用)/ Authorizations(Success/Failure)/ Interchange and Fees。每笔交易须带唯一标识符(支撑无原交易引用的退款对账匹配)。
- 当前为 Excel 格式、为 Astratech 定制;可先共享现有 mBank recon 文件格式作样例。暂无 UAT 环境可测 recon/settlement(若 Scheme 提供则同步)。

### 结算机制
- 频率 每日一次,UAE 4 AM 日切,每日仅一个批次,4 AM 接收结算文件。
- 周末/假日:文件照常生成,处理仅工作日。
- **不支持** split settlement / T+1 部分结算。
- 结算币种 AED;Botim 需提前 pre-fund 到 mBank 账户;CBUAE 侧由 mBank + mBank Operations 完成(有自动扣款)。
- 执行路径:Astratech 依每日 advisement 在 MBank 预存资金 → MBank 通过 CBUAE 向 Jaywan Scheme 结算 → Scheme Settlement 与 Internal Settlement 文件对齐。
- 所有交易须按 Jaywan scheme code 归类以保证清分准确。

### Advisement 与争议
- mBank Operations(Mahesh)每日提供 advisement:total debit / total credit / net position / currency breakdown。
- 对账差异须当日 **14:00 GST 前**提出;否则按原文件完成最终结算。延迟结算罚则通过 pre-fund 规避。

### 退款 / 取消的体现
- 退款、取消通过 settlement file 下发,与原交易同一文件分项展示。
- 退款与原交易关联取决于 acquirer:可能带 reference,也可能不带(无 reference 时以 credit transaction 出现,不关联原交易)。
- 退款发生时 **IRF 被回收(debit)** 到 mBank/Botim,并征收 processing fee。

## 4. 费用与 Chargeback

### 交换费(Interchange)与 VAT
- 不同 MCC 的 Interchange 费率由 Jaywan scheme 规定(详见 Jaywan manual);按交易在对账报告体现(`Interchange Recon Fee Amount` / `Interchange Percentage`)。
- POS 交易 IRF 不收 VAT;ATM 手续费向持卡人收取的 VAT 透传到 customer account。
- 附加费用(如 project fee):单独开票,不从结算账户扣除。

### Chargeback 流程
- 由 BOTIM 提出(将 chargeback 详情 + 客户签署文件以 form/email 发给 Mbank);Mbank Operations 通过 **CBUAE Portal** 代为录入与跟进。Astratech 是否需直接访问 CBUAE Portal 待确认。
- SLA 基于交易量另行定义。
- 文件呈现:chargeback 包含在 settlement file 内但单独分项展示(与 purchases/refunds/cancellations/declined 同文件);Chargebacks & Fee 不单独出文件。结算层面 chargeback 与正常交易分开结算。
- 通用拒付链路(多渠道 VISA/MASTERCARD/MAGNATI/CKO-HISTORY 文件解析、ARN/instOrderNo/authCode 多维匹配)属公司收单 chargeback 体系,落库表 `cmf.tt_inst_order` / `grc.t_payment_event` / `reconciliation.t_clear_flow` / `mchtsettle.t_clearing_item`。详见在线收单域的 chargeback 处理流程(待补对象,本域不展开)。

## 5. 门户与报表(Portal & MIS)

### Astratech 内部门户能力(Card Management Service Portal)
- 卡片挂失/冻结(Blocking);查看用户交易历史(建议 1 个月,提供每日 dump 文件);Chargeback case 提交跟踪(实际在 CBUAE Portal);卡发行/状态/活动 Dashboard;每日/每月报表下载(Excel/CSV,6 个月交易日志视图)。
- mBank 为 Astratech BIN Range 单独启用一套定制 Portal。

### 报表清单(MBank / Dgpays 经 Portal & SFTP 共享)
- 发卡:New Cards / Replacements-Reissuance / Card Closure / Active & Inactive / Merchant Usage。
- 每日结算:Number of Transactions、Settlement Currency、Transactions Amount、Interchange、Billing Currency、Cardholder Billing Amount。
- 清算:Settlement Status、Daily settlement count & spend、Refund Count & spend、Transaction Type、Interchange Recon Fee Amount、Interchange Percentage、AED 与 NON-AED。
- 授权:每日交易总数、成功交易数/金额、Decline transaction Report、3DS Transaction report(如启用)。
- 卡量:Virtual/Physical 卡日/月量、Active Cards monthly、Apple/Google token 总量(如启用)。
- 交易最终授权由 Botim 完成(风控引擎决策,必要时拒绝);需与 DGPAY 明确响应时间。

## 6. 产品矩阵与产品设置
- 卡设计:遵循 Jaywan guidelines(待接收)+ Eproof approval;个性化字段(卡面、欢迎信)。
- 产品设置:BIN Configuration、Program definition、Product type definition、Currency=AED、Pin try limit=3、Card generation=random、PIN Delivery=Green、Card Expiry=5 Years(MM/YY)、Plastic code。
- 产品类型:虚拟卡 + 实体卡,均经 Botim app 发行,支持完整生命周期。
- 限额:按产品维度配置,与交易权限(ECOM/POS/ATM)和 MCC 限制动态控制相关。

## 7. 集成范围(High Level Scope)
- MBank 提供 BIN Sponsorship 与卡管理 API;同时支持虚拟卡与实体卡;Botim 管钱包余额并发起最终授权;MBank 通过 SFTP 每日提供 Excel 对账文件;集成 3DS、Tokenization、交易监控。
- 卡能力:Botim App 发卡 + 配送追踪;Apple Pay/Google Pay tokenization;PIN 创建/更新;完整生命周期(block/activate/replace/renew/closure);动态交易权限 ECOM/POS/ATM;MCC 限制;3DS 电商;实时余额更新查询;退款/冲正/拒付/对账。货币 AED。

## 8. 上线依赖(Dependencies & Action Points)
- MBank 为 Astratech program 启用 BIN;Dgpays 在 pre-prod 暴露最终 API;Settlement process 签署;Courier partner 确认就绪;SLA 签署;Product setup 完成。
- 利益相关方:MBank(BIN Sponsor)、Dgpays(处理方/对账文件)、Astratech/Botim(钱包余额/最终授权/客服运营门户)、Jaywan Scheme/CBUAE(清结算通道)、Courier Partner(实体卡寄送)。

## QA 关注点
- 三环境(SIM/UAT/PROD)配置一致性:商户号、网关 URL、ProductNumber/SubProductNumber、BIN、费率、限额、MCC、错误码(配置漂移风险)。
- 密钥链路:公私钥生成、Key Vault 路径正确、加解密方向(请求用对端公钥加密 / 响应用己方私钥解密)。
- 对账:T+1 文件字段完整性、唯一标识符、无 reference 退款的 credit transaction 匹配、IRF 回收 + processing fee、争议 14:00 GST 截止。
- 结算:pre-fund 充足性、AED 单批日结、scheme code 归类正确、不支持 split settlement 的边界。
- Chargeback:BOTIM→Mbank→CBUAE Portal 链路状态/回执/SLA 计时可追踪;settlement 文件中 chargeback 分项识别;chargeback 单独结算。
