---
id: reference_ppc_card_apis
object_type: Reference
name: PPC 卡 API 清单 / 错误码 / 测试用例生成指引
aliases: [PPC API inventory, ppc-api-card-management, ppc-api-transaction, ppc-api-error-codes]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2133098640 (PPC 核心 API 清单 / 错误码 / 用例生成指引)
tags: [ppc, card, api, error-codes, test-generation]
related_services: [svc_ppc, svc_cgs]
---

# PPC 卡 API 清单 / 错误码 / 测试用例生成指引

> PPC 卡业务对外/内部 API 的事实来源,供 AI/QA 推导接口与集成测试用例(覆盖度、字段边界、错误码反向、幂等、跨 API 串联、异步时序)。Path 多为推断格式,待后端确认。实时接口文档:`https://sim-admin.corp.test2pay.com/api-doc/`(Smart-doc 自动生成)。
> 关联:卡生命周期状态机与转换用例见 [[scn_card_lifecycle_transitions]];端到端流程见 [[flow_ppc_card_lifecycle]]。

## API 网关
| 网关 | 用途 | App / 服务 |
| --- | --- | --- |
| CGS (Client Gateway Service) | App / Web / H5 调用 | gp024_cgs([[svc_cgs]]) |
| SGS (Server Gateway Service) | 内部服务 / 商户调用 | gp028_sgs |

## 卡管理 API(前缀 `/ppc/card/v1/`,调用方 App)
| 操作 | Method | Path(推断) | 关键字段 | 幂等键 / 限制 |
| --- | --- | --- | --- | --- |
| 获取卡概览 | GET | `/summary` | `member_id` | — |
| 申请虚拟卡 | POST | `/apply-virtual` | `member_id`, `card_type`(MC/PR), `kyc_token` | `member_id + card_type + session_id`;前置 KYC 通过否则 `KYC_NOT_VERIFIED` |
| 设置 PIN | POST | `/set-pin` | `virtual_card_id`, `pin`(encrypted), `confirm_pin`, `identity_verify_token` | PIN 必加密 |
| Reset PIN | POST | `/reset-pin` | `virtual_card_id`, `pin`, `identity_verify_token` | 调 APIPTR 解锁 PIN |
| 查看卡明细 | GET | `/detail` | `virtual_card_id`, `identity_verify_token` | — |
| 查看卡号 (PAN) | GET | `/pan` | `virtual_card_id`, `identity_verify_token` | 走 YSE 查询接口 |
| 锁卡 | POST | `/lock` | `virtual_card_id`, `identity_verify_token` | `virtual_card_id + operate_session_id`(弱网防重复,BUG-6548) |
| 解锁卡 | POST | `/unlock` | 同上 | 同上(BUG-6554) |
| 替换卡 | POST | `/replace` | `virtual_card_id`, `identity_verify_token` | 累计 ≤ 3 次,第 4 次必拒 |
| 关闭卡(用户) | POST | `/close` | `virtual_card_id`, `identity_verify_token`, `close_reason` | `virtual_card_id + close_session_id`;关卡前余额必清零,否则 `NON_ZERO_BALANCE` |
| 实体卡申请初始化 | POST | `/init-apply-physical` | `virtual_card_id` | 返回默认地址 + 名称 |
| 实体卡申请提交 | POST | `/apply-physical` | `virtual_card_id`, `card_holder_name`(≤25), `delivery_address`, `card_style`(Standard/Metal) | 关闭未支付旧订单 |
| 跟踪实体卡 | GET | `/tracking-physical-card-order` | `order_id` | 字段 `mobilePhoneNumber`(BUG-6892), `fees`(BUG-6893) |
| 激活实体卡 | POST | `/activate` | `virtual_card_id`, `proxy_number` | 卡状态校验 = `UNACTIVATED` |

## 交易 / 账务 API
| 操作 | Method | Path(推断) | 调用方 | 备注 |
| --- | --- | --- | --- | --- |
| 查询交易明细 | GET | `/ppc/card/v1/transactions` | App | — |
| 充值 (add funds) | POST | `/ppc/card/v1/add-funds` | App | 重复请求幂等 |
| 货币转换 | POST | `/ppc/fx/v1/convert` | App | — |
| 汇率试算 | POST | `/ppc/fx/v1/calculate` | App | 弱网键盘关闭后不应调用(BUG-6529) |
| 下载交易单 | GET | `/ppc/card/v1/statement` | App / H5 | 失效 token 必拒 |

交易类型枚举 `T/S/R/RL/F/CB/RF/FRL` 定义见外部参考 `ppc-OP-3-Fee Config`;账务细节见 `ppc-SD-3-Transaction`。

## 卡组织接口(出向 YSE / Jaywan)
- **Authorization (APIAUT)** — 授权报文;`ResponseCode=75` 表示 PIN locked。
- **PIN Tries Reset (APIPTR)** — 解锁 PIN。
- **Card Status Update** / **Update Card Detail** — 卡状态/信息变更通知(入向)。

## 卡组织 / 物流回调(入向)
| 事件 | Method | Path(推断) | 触发方 | 处理动作 |
| --- | --- | --- | --- | --- |
| Authorization | POST | `/ppc/yse/notify/auth` | YSE/Jaywan | 校验余额、写授权流水、设置 Pending Account |
| Clearing / Settle | POST | `/ppc/yse/notify/clearing` | YSE/Jaywan | Pending → Settle / Refund / Reversal |
| PIN Locked | POST | `/ppc/yse/notify/pin-lock` | YSE | 标记 PIN locked |
| Card Detail Update | POST | `/ppc/yse/notify/card-update` | YSE | 同步本地卡数据 |
| Trade Notify | POST | `/ppc/trade/notify` | trade 服务 | 实体卡支付完成 → 推 YSE 制卡 / 关卡 |
| Shipment Notify | POST | `/ppc/usp/notify/shipment` | USP/Jeebly | 配送状态变更 |
| Biometrics Notify | POST | `/ppc/usp/notify/biometrics` | USP | 生物信息上传 |
| Jeebly Delivery Status | POST | `/ppc/api/jeebly/delivery-status` | Jeebly | 状态:Out for delivery / Delivered / Cancelled / RTO Delivered(**BUG-8948 RTO 处理报错**) |

## 通用错误码
| Code | 含义 | 触发场景 | 测试用例提示 |
| --- | --- | --- | --- |
| `INVALID_CARD_STATUS` | 卡状态不允许该操作 | 已销卡操作 / 申请中激活 / Closing 中再操作 | 反向状态用例必含 |
| `NON_ZERO_BALANCE` | 余额非零禁止关卡 | 关卡前未清零 | 必出资损用例 |
| `VIRTUAL_CARD_NOT_EXIST` | 虚拟卡不存在 | 错误 ID / 异步消息延迟 | — |
| `VIRTUAL_CARD_TYPE_NOT_EXIST` | 卡类型未配置 | BIN 路由异常 | — |
| `PROCESSING_EXCEPTION` | 处理异常 | 上下游异常(YSE/trade/grc) | 重试机制需测试 |
| `SYSTEM_EXCEPTION` | 系统异常 | 兜底 | 必测降级 |
| `KYC_NOT_VERIFIED` | KYC 未通过 | 申请卡前置校验 | 必测 |
| `IDENTITY_VERIFY_FAILED` | 核身失败 | 敏感操作前置 | 必测 |
| `ResponseCode 75` | PIN Locked(来自 YSE Authorization) | 用户 PIN 连续输错达上限 | PIN 解锁回归 |

## 测试用例生成指引(六大维度)
1. **API 覆盖度**:每个 API ≥1 条正向;每个声明的错误码 ≥1 条反向。
2. **字段边界**:金额(精度/边界/负数);字符串(长度边界,如 `card_holder_name` ≤25、特殊字符);币种(合法/非法 ISO);PAN/CVV/PIN 必加密传输。
3. **幂等性**:每个标注幂等键的 API 必出 1 条重复请求用例 → 返回相同结果、DB 不创建新记录。典型幂等键:apply-virtual(`member_id+card_type+session_id`)、lock/unlock(`virtual_card_id+operate_session_id`)、close(`virtual_card_id+close_session_id`)。
4. **串联链路**:5-API 虚拟卡链路(申请→激活→锁→解锁→关闭);6-API 实体卡链路(申请实体卡→支付→制卡→配送→激活)。需校验跨服务状态一致性。
5. **回调时序(异步)**:乱序(Clearing 先于 Authorization)、重投、丢失、超时 → 必测幂等 + 兜底对账;非法状态跃迁(Pending→Settle/Refund/Reversal)必拒;签名/来源校验。
6. **核身依赖**:所有需 `identity_verify_token` 的 API,失效/伪造/过期 token 必返回 `IDENTITY_VERIFY_FAILED` 且必拒。

### 特殊业务规则用例
- 关卡:余额非零禁止关闭 → `NON_ZERO_BALANCE`(资损红线)。
- 替换卡:累计 ≤ 3 次,第 4 次必拒。
- 激活实体卡:仅当卡状态 = `UNACTIVATED` 才允许。
- PIN Locked:YSE Authorization 返回 `ResponseCode=75` → 调 APIPTR 解锁,必做回归。
- FX 试算:弱网键盘关闭后不应再调用(回归 BUG-6529)。
- Jeebly Delivery Status:四种状态各 1 条正向 + RTO 异常路径回归(BUG-8948)。

## 用例规模估算
30+ APIs × 平均 4 条(happy + 错误码 + 边界 + 幂等)≈ **~120 条** API 层用例(不含跨链路/异步时序组合)。

## 外部参考
- `ppc-SD-3-Transaction`(Authorization / Clearing / Reversal 账务细节)
- `ppc-OP-3-Fee Config`(交易类型枚举 T/S/R/RL/F/CB/RF/FRL)
- `ppc-SD-Processor API`(卡组织接口源)
- `ppc-2-流程图设计`(各流程服务交互图)
