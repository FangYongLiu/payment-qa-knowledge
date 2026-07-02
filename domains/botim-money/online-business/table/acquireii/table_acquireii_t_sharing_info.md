---
id: tbl_acquireii_t_sharing_info
object_type: Table
name: 分账信息表 (t_sharing_info)
aliases: [t_sharing_info, acquireii.t_sharing_info]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: acquireii schema DDL
tags: [online-business, 收单, acquireii]
sensitivity: normal
related_services: [svc_acquireii]
---

# 分账信息表 (t_sharing_info)

## 用途
物理表 `acquireii.t_sharing_info`,主键 `id`。分账信息表。属收单服务 [[svc_acquireii]]。业务语义细节**待补**(表结构来自 DDL,用途需结合代码/文档补充)。

## 关联关系
- **所属服务**:[[svc_acquireii]](= `related_services`)。
- **谁读写它**:收单链路的服务 / 接口(由对方文档的 `related_tables` 声明,本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 通用指令id |
| `order_type` | varchar(32) | 订单类型 |
| `order_id` | bigint | 订单ID |
| `sharing_identity` | varchar(200) | 分账标识 · 可空 |
| `sharing_currency_code` | varchar(8) | 分账币种 |
| `sharing_mid` | varchar(32) | 分账会员ID |
| `sharing_identity_seq_id` | int | 标志序号 |
| `sharing_memo` | varchar(128) | 分账备注 |
| `sharing_identity_type` | varchar(16) | 分账标识类型 |
| `sharing_amount` | decimal(19,4) | 收单金额 |
| `created_time` | timestamp(3) | 创建时间 |
| `sharing_settled_crcy` | char(3) | 分账结算币种 · 可空 |
| `sharing_settled_amount` | decimal(19,4) | 分账结算金额 · 可空 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `sharing_settled_fee_crcy` | char(3) | 分账结算手续费币种 · 可空 |
| `sharing_settled_fee_amt` | decimal(19,4) | 分账结算手续费金额 · 可空 |
| `withhold_and_remit_fee` | varchar(8) | withholdAndRemitFee · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_si_ct`:created_time
- `i_si_oi`:order_id

## 校验点(QA 关注)
- **时间字段**:`created_time`=入库、`last_updated_time`=最后更新;按时间过滤走对应索引,勿混用。
- **乐观锁**:更新须带 `data_version`,并发场景校验版本递增、防覆盖。
- **金额精度**:decimal 金额比较用容差(< 0.01);相关币种字段应一致。
- **关联订单**:`order_id` 关联收单/退款主单(结合 `order_type` 判断单据类型)。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
