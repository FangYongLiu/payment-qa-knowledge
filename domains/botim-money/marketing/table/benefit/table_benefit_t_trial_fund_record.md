---
id: tbl_benefit_t_trial_fund_record
object_type: Table
name: t_trial_fund_record (t_trial_fund_record)
aliases: [t_trial_fund_record, benefit.t_trial_fund_record]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: benefit schema DDL
tags: [marketing, benefit]
sensitivity: normal
related_services: []
---

# t_trial_fund_record (t_trial_fund_record)

## 用途
物理表 `benefit.t_trial_fund_record`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键自增 · 可空 |
| `member_id` | varchar(32) | 会员id |
| `trial_fund_id` | bigint | 体验金id |
| `trial_days` | int(10) | 待补 |
| `trial_amount` | decimal(19, 4) | 体验金金额 |
| `currency` | char(3) | 币种 |
| `status` | varchar(10) | 状态： 已领取:R   已激活:A   无效:N |
| `receive_time` | timestamp | 领取时间 · 可空 |
| `activate_time` | timestamp | 激活时间 · 可空 |
| `activate_expire_time` | timestamp | 激活到期时间 · 可空 |
| `trial_expire_time` | timestamp | 体验到期时间 · 可空 |
| `close_time` | timestamp | 用户关闭时间 · 可空 |
| `expire_time` | timestamp | 数据过期时间 |
| `message` | varchar(255) | 记录信息 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `idx_expire_time`:expire_time
- `idx_member_id_expire_time`:member_id, expire_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
