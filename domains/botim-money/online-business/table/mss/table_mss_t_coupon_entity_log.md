---
id: tbl_mss_t_coupon_entity_log
object_type: Table
name: 券操作记录表 (t_coupon_entity_log)
aliases: [t_coupon_entity_log, mss.t_coupon_entity_log]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mss schema DDL
tags: [online-business, mss]
sensitivity: normal
related_services: []
---

# 券操作记录表 (t_coupon_entity_log)

## 用途
物理表 `mss.t_coupon_entity_log`,主键 `log_id`。券操作记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `log_id` | int | 主键 · 可空 |
| `coupon_entity_id` | bigint | 权益实体类型 |
| `coupon_no` | varchar(64) | 券号 按照一定的算法实现 |
| `coupon_random` | varchar(32) | 券随机数 · 可空 |
| `award_group_id` | int | 奖品组id · 可空 |
| `award_item_id` | bigint | 奖品模板id |
| `activity_code` | varchar(128) | 活动id |
| `tool_id` | int | 工具id · 可空 |
| `member_id` | varchar(64) | 会员号 · 可空 |
| `coupon_type` | varchar(32) | 券类型 比例，定额 |
| `coupon_attr` | char(4) | d-可叠加，s-单张使用 |
| `link_url` | varchar(128) | 跳转地址 · 可空 |
| `award_url` | varchar(255) | 实物奖品url · 可空 |
| `coupon_amount` | decimal(8, 4) | 券额度 定额时必须 · 可空 |
| `coupon_percent` | decimal(8, 4) | 折扣比例 比例时必须 · 可空 |
| `discount_amount` | decimal(8, 4) | 折扣金额 · 可空 |
| `account_no` | varchar(64) | 账户号 券对应出金账户 · 可空 |
| `account_type` | varchar(64) | 账户类型 · 可空 |
| `currency` | char(3) | 币种 定额时必须 · 可空 |
| `batch_no` | varchar(64) | 批次号 后台每次发券时产生 · 可空 |
| `use_threshold` | decimal(8, 4) | 使用门槛 -1无门槛 |
| `effective_time` | timestamp | 生效时间 |
| `expire_time` | timestamp | 过期时间 |
| `request_no` | varchar(64) | 请求号 · 可空 |
| `op_type` | varchar(32) | 操作类型：lock-冻结，used-核销，unlock-解锁 |
| `merchant_id` | varchar(64) | 交易商户id · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 创建时间 |
| `remarks` | varchar(128) | 备注 · 可空 |
| `account_mid` | varchar(64) | 账户mid · 可空 |
| `trade_amount` | decimal(12, 4) | 交易金额 · 可空 |
| `upper_limit` | decimal(8, 4) | 折扣上限 · 可空 |
| `coupon_source` | varchar(32) | 来源 · 可空 |

## 主键 / 索引
- 主键:`log_id`
- `idx_coupon_no`:coupon_no
- `idx_request_no`:request_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
