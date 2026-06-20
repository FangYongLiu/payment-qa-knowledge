---
title: 收单订单查询慢SQL优化技术方案
domain: acquire-transaction
kind: wiki_page
slug: acquire-order-slow-sql-optimization
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:cbd444e6-2193-4675-89e8-bfa0439bece7
tags: []
---

# 收单订单查询慢SQL优化技术方案

针对 `t_acquire_order` 大商户场景下时间范围查询出现慢SQL的问题，从扫描行数、链路隔离、近似计数、热点分表四个维度提出优化思路，最终选择"约束查询时间范围 + 新建查询服务走从库"的组合方案落地。

## 问题背景

- 入口：商户Portal 查询收单信息，支持按时间范围检索
- 触发条件：时间范围 > 1 个月时出现慢查询
- 涉及表：`t_acquire_order`、`t_secondary_merchant_detail`、`t_payment_info`

## 慢SQL分析

典型慢查询语句（count 分页统计）：

```sql
select count(acquireord0_.global_id) as col_0_0_
from t_acquire_order acquireord0_
left outer join t_secondary_merchant_detail secondarym1_
  on acquireord0_.global_id = secondarym1_.global_id
cross join t_payment_info paymentinf2_
where acquireord0_.global_id = paymentinf2_.global_id
  and acquireord0_.ttlamt_currency_code = 'AED'
  and acquireord0_.partner_id = '200010278881'
  and acquireord0_.created_time >= '2024-01-01 00:00:00.0'
  and acquireord0_.created_time <= '2024-08-28 23:59:59.0'
  and paymentinf2_.pay_channel = 'NYU_STUDENT_CARD';
```

数据分布：

- 扫描行数：26,289,941
- 全表行数：53,964,702
- 热点商户 `partner_id=200010278881` 在全表中记录数 41,838,730，占比 **77%**

根因：命中该 `partner_id` 条件且数据量大时必然引发慢查询。

## 优化思路对比

### 思路一：约束查询时间范围，减少扫描数据量

实测耗时（按时间窗口）：

| 时间范围 | 查询耗时 | 数据量 |
|---|---|---|
| 2 周 | 2.94s | 1,020,499 |
| 1 月 | 5.56s | 1,907,417 |
| 2 月 | 12.02s | 4,185,323 |

- 与产品确认：查询范围可限制在 1 个月以内，1 个月以外的数据考虑**归档**
- 效果预估：分页查询耗时从 >30s 降至约 10s；若需做到秒级响应，需进一步缩小时间窗口

### 思路二：新建查询服务，走从库读取

- 收单服务本身支持多数据源，但基于 JPA 框架改造影响面大，可能影响主链路稳定性
- 非收单链路后续可能出现更多复杂查询，考虑**新建独立数据查询服务**统一对外提供
- 效果预估：避免非核心链路影响主链路；降低慢查对主库的冲击
- 与思路一不冲突，可并行实施

### 思路三：百万级以上结果集返回近似值

- 当结果集达百万 / 千万量级且业务可接受一定误差时，可用**扫描行数作为近似总记录数**返回
- 需确认业务可行性
- 效果预估：减少一次 count 查询耗时（约 5s）

### 思路四：热点 partner_id 拆分独立表

- 针对 `partner_id=200010278881`（占 77%）做独立分表存储
- 成本：数据迁移 + 应用层查询路由改造
- 效果预估：热点商户操作不影响其他用户数据查询

## 落地方案

综合改造效果、稳定性保障与成本考量，采用 **思路一 + 思路二** 组合落地。

任务拆解：

- Jira 申请新项目
- 搭建项目，迁移查询接口 — 1 day
- 上游调用方接口切换 — 1 day
- 上下游联调（SIM、UAT 环境测试）— 2 day
- Buffer — 1 day
