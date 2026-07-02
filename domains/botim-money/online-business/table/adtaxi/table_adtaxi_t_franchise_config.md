---
id: tbl_adtaxi_t_franchise_config
object_type: Table
name: 出租车加盟配置表 (t_franchise_config)
aliases: [t_franchise_config, adtaxi.t_franchise_config]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: adtaxi schema DDL
tags: [online-business, 出租车支付, adtaxi]
sensitivity: normal
related_services: [svc_adtaxi]
---

# 出租车加盟配置表 (t_franchise_config)

## 用途
物理表 `adtaxi.t_franchise_config`,主键 `id`。出租车配置。属出租车支付服务 [[svc_adtaxi]]。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:[[svc_adtaxi]](= `related_services`)。
- **谁读写它**:出租车支付链路的服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `franchise` | varchar(64) | 待补 |
| `franchise_type` | varchar(8) | inner标识 |
| `payee_mid` | varchar(32) | 收款人mid |
| `created_time` | timestamp(3) | 创建时间 |
| `icon_url` | varchar(128) | iconUrl · 可空 |
| `secondary_merchant_no` | varchar(128) | secondaryMerchantNo · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_fr_fc`:franchise (UNIQUE)
- `uk_fr_smn`:secondary_merchant_no (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:`created_time`=入库、`last_updated_time`=最后更新;按时间过滤走对应索引。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
