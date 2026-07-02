---
id: tbl_marketorder_t_auto_recharge_config
object_type: Table
name: 自动充值配置表 (t_auto_recharge_config)
aliases: [t_auto_recharge_config, marketorder.t_auto_recharge_config]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketorder schema DDL
tags: [marketing, marketorder]
sensitivity: normal
related_services: []
---

# 自动充值配置表 (t_auto_recharge_config)

## 用途
物理表 `marketorder.t_auto_recharge_config`,主键 `id`。自动充值配置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 |
| `open_id` | bigint(18) | 开通id |
| `member_id` | varchar(18) | 会员id |
| `partner_id` | varchar(32) | 平台ID · 可空 |
| `platform_type` | varchar(15) | 终端类型 |
| `account_id` | bigint(18) | 账户id |
| `goods_code` | varchar(20) | 商品code · 可空 |
| `sku_code` | varchar(20) | sku_code · 可空 |
| `amount` | decimal(10, 2) | 充值金额：为空代表账单全部金额 · 可空 |
| `currency` | varchar(10) | 币种 |
| `config_status` | varchar(10) | 配置状态：CLOSE（关闭），OPEN（打开） |
| `status` | varchar(4) | 有效：Y 无效：N |
| `recharge_date` | timestamp | 下一次充值日期 · 可空 |
| `auto_payment_day` | varchar(8) | 几号 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
