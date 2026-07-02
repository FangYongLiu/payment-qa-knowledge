---
id: tbl_assetinfo_t_trade_limit
object_type: Table
name: 交易限制 (t_trade_limit)
aliases: [t_trade_limit, assetinfo.t_trade_limit]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: assetinfo schema DDL
tags: [lending, assetinfo]
sensitivity: normal
related_services: []
---

# 交易限制 (t_trade_limit)

## 用途
物理表 `assetinfo.t_trade_limit`,主键 `asset_code`。交易限制。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `asset_code` | varchar(32) | id |
| `fiat_buy_minimum` | decimal(23, 8) | 法币买单最小金额 |
| `fiat_buy_maximum` | decimal(23, 8) | 法币买单最大金额 |
| `asset_buy_minimum` | decimal(23, 8) | 资产买单最小金额 |
| `asset_buy_maximum` | decimal(23, 8) | 资产买单最大金额 |
| `fiat_sell_minimum` | decimal(23, 8) | 法币卖单最小金额 |
| `fiat_sell_maximum` | decimal(23, 8) | 法币卖单最大金额 |
| `asset_sell_minimum` | decimal(23, 8) | 资产卖单最小金额 |
| `asset_sell_maximum` | decimal(23, 8) | 资产卖单最大金额 |
| `buy_status` | varchar(16) | 待补 |
| `sell_status` | varchar(16) | 待补 |
| `trade_precision` | bigint | trade_precision |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `vip_fiat_buy_minimum` | decimal(23, 8) | vip法币买单最小金额 · 可空 |
| `vip_fiat_buy_maximum` | decimal(23, 8) | vip法币买单最大金额 · 可空 |
| `vip_asset_buy_minimum` | decimal(23, 8) | vip资产买单最小金额 · 可空 |
| `vip_asset_buy_maximum` | decimal(23, 8) | vip资产买单最大金额 · 可空 |
| `vip_fiat_sell_minimum` | decimal(23, 8) | vip法币卖单最小金额 · 可空 |
| `vip_fiat_sell_maximum` | decimal(23, 8) | vip法币卖单最大金额 · 可空 |
| `vip_asset_sell_minimum` | decimal(23, 8) | vip资产卖单最小金额 · 可空 |
| `vip_asset_sell_maximum` | decimal(23, 8) | vip资产卖单最大金额 · 可空 |

## 主键 / 索引
- 主键:`asset_code`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
