---
id: tbl_remittance_t_channel_market
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_channel_market
subdomain: remittance
module: null
sensitivity: normal
name: 渠道营销(t_channel_market)
aliases:
- t_channel_market
related_services:
- svc_remittance
related_scenarios: []
---
# 渠道营销(t_channel_market)

## 用途
渠道营销。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID;前8后9 |
| `order_no` | bigint | NOT NULL | 汇款订单号 |
| `channel_code` | varchar(12) | NOT NULL | 渠道编号;MG |
| `market_type` | varchar(12) | NOT NULL | 营销类型;CFW：corridor fee waiver |
| `market_key` | varchar(64) | NOT NULL | 营销关键字;如收款方全名+accountNo |
| `member_id` | varchar(20) | NOT NULL | 会员号;汇款人会员号 |
| `country_code` | char(2) | NOT NULL | 汇款目标国家 |
| `transaction_mode` | varchar(20) | NOT NULL | 汇款模式 |
| `corridor_fee` | decimal(15,4) |  | 优惠通道费 |
| `cashback_amount` | decimal(15,4) |  | 返佣金额 |
| `currency` | char(3) | NOT NULL | 币种 |
| `status` | tinyint | NOT NULL | 状态;-1-无效，0-待定，1-有效 |
| `memo` | varchar(100) |  | 备注 |
| `extension` | varchar(255) |  | 扩展信息 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
