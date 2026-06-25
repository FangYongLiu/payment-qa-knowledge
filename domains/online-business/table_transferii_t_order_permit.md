---
id: tbl_transferii_t_order_permit
object_type: Table
name: 订单收款凭证表 (t_order_permit)
aliases: [t_order_permit, Collect Permit]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: wiki_image:654d5bef-1e1a-485d-a44b-c83918b7165b
tags: [transferii, send-money, collect-permit]
related_services: []
related_scenarios: []
---

# 订单收款凭证表 (t_order_permit)

## 用途
位于 `transferii` schema,存放钱包订单的 Collect Permit(收款许可凭证)。每条记录通过 `wallet_order_no` 关联主表 [[tbl_transferii_t_wallet_order]],标识收款方可凭何种凭证(如手机号、邮箱等)领取该笔钱包订单资金。流程见 [[flow_wallet_send_money]]。

## 关联关系
- **所属服务**:transfer(待补,未建 Service 对象)
- **关联主表**:[[tbl_transferii_t_wallet_order]](`wallet_order_no` FK)
- **同模型表**:[[tbl_transferii_t_party_order]]、[[tbl_transferii_t_cancel_order]]

## 关键列
| 列名 | 含义 | Key | 类型 | 长度 |
|---|---|---|---|---|
| permit_id | Permit ID | PK | bigint | - |
| wallet_order_no | 关联钱包订单 | FK | bigint | - |
| permit_type | 凭证类型 | - | char | 1 |
| permit_value | 凭证值 | - | varchar | 32 |

## 主键 / 索引
- 主键:`permit_id`
- 外键:`wallet_order_no` → `t_wallet_order.wallet_order_no`

## 校验点(QA 关注)
- `wallet_order_no` 必须存在于 `t_wallet_order`(外键完整性)。
- `permit_type`(char1):需校验取值集合是否被业务白名单约束(原文未列举具体编码,测试时对照实际枚举)。
- `permit_value`(varchar32):超长输入应被拒绝;不同 `permit_type` 对应的格式(如手机号、邮箱)需符合各自校验规则。
- **类型不一致风险**:主表 `wallet_order_no` 为 varchar(32),本表标注 bigint,是潜在数据质量/JOIN 风险点,QA 应确认 schema 与实际实现是否对齐。
- 一个 `wallet_order_no` 可能对应多条 permit(多凭证场景),需验证唯一性约束与重复插入处理。
