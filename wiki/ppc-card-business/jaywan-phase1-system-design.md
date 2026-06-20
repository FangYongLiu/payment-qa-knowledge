---
title: Jaywan Phase1系统设计任务
domain: ppc-card-business
kind: wiki_page
slug: jaywan-phase1-system-design
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:b4ddb781-c8c9-4531-9714-54f78aa19fea
tags: []
---

# Jaywan Phase1系统设计任务

本页汇总 Jaywan 预付卡 Phase 1（含 Phase 1 主体与 Clearing & Settlement）的开发任务清单，含模块、对应 Dgpay/Institution API、优先级、工作量与负责人。完整产品上下文见 [[jaywan-prepaid-card-overview]]，端到端用例见 [[jaywan-use-case-list]]。

## 范围与说明

- Phase 1 覆盖优先级 0、1、2 的任务；优先级 3 为后续/恢复类增强。
- 设计文档前缀：`gppc-SD-Jaywan Basic / Virtual Card / Physical Card / Transaction / Clearing & Settlement`。
- 清结算细节单独整理见 [[jaywan-clearing-settlement-design]]；Phase 2 任务见 [[jaywan-phase2-system-design]]。
- 端到端业务流程参见 [[flow_jaywan_card_lifecycle]]。

## Basic（基础能力）

| 任务 | Dgpay API | 要点 | 优先级 | 工作量 | 负责人 |
|---|---|---|---|---|---|
| Key Management - 90% | - | Inner api 获取 key；加解密 api；参考 Encryption Process（Wiki: gppc-OP-Key Generation） | 0 | 1.5d | huihua.ni |
| Apply vendor token - 100% | GetToken | Inner API；管理 vendor token；过期前异步生成新 token；统一 api 请求流程（token 附加、pojo 转换）；单测 mock vendor responder | 0 | 3d | huihua.ni |
| Generate institution token - 90% | Inst GetToken | Institution API；生成与管理 institution token；统一 api 响应流程（token 校验、pojo 转换）；单测 mock vendor requester | 1,2 | 2d | yu.tang |

## Virtual Card（虚拟卡）

| 任务 | Dgpay API | 要点 | 优先级 | 工作量 | 负责人 |
|---|---|---|---|---|---|
| Apply virtual card - 100% | CreatePrepaidDigitalCard | CGS API：Summary Query、Init Apply、Apply | 0 | 3d | yu.tang |
| Query Card Info - 90% | GetPrepaidCards | CGS API：View Card Detail | 0 | 0.5d | yu.tang |
| PIN Set - 80% | PrepaidCardPinOperation | CGS API：Set Card PIN | 0 | 1d | yu.tang |
| Lock/Unlock Card - 100% | UpdatePrepaidCardStatus | CGS API：Lock / Unlock Card | 0 | 0.5d | yu.tang |
| Apply virtual card - recovery - 100% | GetPrepaidCards | 通过 GetPrepaidCards 自动从 vendor error 恢复 | 3 | 0.5d? | yu.tang |
| Update Mobile - 100% | UpdateMobilePhoneNumber | 手机号变更时同步至 dgpay | 3 | 0.5d? | yu.tang |
| Update status from bank portal - 90% | Inst: UpdatePrepaidCardStatus | Institution API | 3 | 0.5d? | yu.tang |
| Apply virtual card with pay - 90% | - | CGS API；with pay 与 with physical card；过期已有未成功申请；与实体卡一起申请；收到交易结果后更新状态并异步申请虚拟卡和实体卡 | 3 | 3d | cong.zhou |

## Physical Card（实体卡）

| 任务 | Dgpay API | 要点 | 优先级 | 工作量 | 负责人 |
|---|---|---|---|---|---|
| Apply physical card - 100% | CreatePrepaidEmbossData | CGS API：Init Apply、Apply、Tracking；支付费用并申请实体卡 | 1 | 3d | huihua.ni |
| Activate Physical Card - 100% | ActivatePrepaidCard | CGS API | 1 | 0.5d | huihua.ni |
| Delivery tracking - 90% | Inst: NotifyCourierProcess | Institution API | 1,2 | 0.5d | yu.tang |
| Apply physical card - recovery | - | 自动从 vendor error 恢复 | 3 | 0.5d? | yu.tang |

## Transaction（交易）

| 任务 | Dgpay API | 要点 | 优先级 | 工作量 | 负责人 |
|---|---|---|---|---|---|
| Provision - 90% | Inst: Provision | Institution API：实现 provision 报文；集成 risk、payment、bill、pns；交易与退款 | 1,2 | 3d | yu.tang |
| Balance Inquery - 90% | Inst: Balance Inquery | Institution API：实现 balance inquery 报文；新增 balance inquery | 1,2 | 0.5d | yu.tang |
| Reversal - 90% | Inst: Reversal | Institution API：实现 reversal 报文；额外重试流程 | 1,2 | 1d | yu.tang |
| Declined Transaction - 100% | Inst: Declined Transactions | Institution API；保存被拒交易；按需发送通知 | 3 | 0.5d? | yu.tang |

## Clearing & Settlement（Phase 1 范围内的清结算）

详细设计见 [[jaywan-clearing-settlement-design]]。Phase 1 涉及任务：

| 任务 | Dgpay API | 要点 | 优先级 | 工作量 | 负责人 |
|---|---|---|---|---|---|
| Clearing file process frame | Clearing File | 清算文件处理框架；伴随 Clearing detail process - DECLINE；在已有流程中加入 settlement detail 生成 | 0 | 2d | yu.tang |
| Clearing detail process - OFFLINE | - | OFFLINE 清算处理 | 1 | 1d | yu.tang |
| Clearing detail process - PROVISION, BALANCE_INQUERY | - | PROVISION、BALANCE_INQUERY 清算处理 | 1 | 2d | yu.tang |
| Clearing detail process - REVERSAL | - | REVERSAL 清算处理；为单报文 reversal 增加冲正结算更新 | 2 | 3d | yu.tang |

> Settlement file generation（优先级 3）、Reconciliation（优先级 4）属 Phase 1 之外的延伸，归入 [[jaywan-clearing-settlement-design]]。

## 相关问答

- 产品侧问题与决议：[[jaywan-product-qa]]
- Vendor (Dgpay) 集成问答：[[jaywan-vendor-qa]]

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>

</br>
