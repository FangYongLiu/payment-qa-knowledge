---
title: 收单服务慢SQL优化技术方案
domain: acquire-transaction
kind: wiki_page
slug: acquire-order-slow-sql-optimization
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/674791436
tags: []
---

# 收单服务慢SQL优化技术方案

针对商户Portal查询收单信息场景下，时间范围超过1个月时出现的慢查询问题，进行根因分析并提出多维度优化思路。

## 问题定义

- **业务场景**：商户Portal查询收单信息，支持用户按时间范围检索
- **触发条件**：时间范围大于1个月时出现慢查询
- **核心表**：`t_acquire_order`，关联 `t_secondary_merchant_detail`、`t_payment_info`

### 慢SQL示例

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

### 数据规模与根因

- 查询扫描行数：**26,289,941**
- 表总行数：**53,964,702**
- 热点商户 `partner_id=200010278881` 在全表占比 **77%**（记录数 41,838,730）
- **根因**：一旦命中该热点 `partner_id` 且数据量过大，必然引起慢查询

## 优化思路

### 思路一：约束查询数据时间范围

通过限制查询时间窗口减少扫描数据量。

测试数据：

| 时间范围 | 查询耗时 | 数据量 |
|---------|---------|--------|
| 2周 | 2.94s | 1,020,499 |
| 1月 | 5.56s | 1,907,417 |
| 2月 | 12.02s | 4,185,323 |

- **产品共识**：查询范围控制在 1 个月以内，更早数据考虑归档
- **效果预估**：分页查询耗时从 >30s 降低至 10s；若需秒级响应，需进一步缩小时间窗口

### 思路二：新增独立查询服务，走从库读取

将非核心查询链路与收单主链路解耦（与思路一可并行）。

- **背景**：收单服务虽然支持多数据源，但 JPA 框架下改动较大，可能影响主链路稳定性
- **方案**：新建独立数据查询服务，统一对外提供查询能力
- **效果预估**：
  - 避免非核心链路影响主链路
  - 降低慢查对主库的影响

### 思路三：大数据量场景返回近似总数

当结果数达到百万、千万量级且业务允许一定误差时，使用扫描行数近似替代精确 count。

- **前提**：需确认业务可行性
- **效果预估**：减少一次 count 查询耗时（约 5s）

### 思路四：热点数据分表

将热点 `partner_id` 数据独立拆分存储。

- **依据**：`partner_id=200010278881` 占全表 77% 数据
- **成本预估**：数据迁移、应用层支持查询路由
- **效果预估**：热点 partner_id 操作不影响其他用户数据查询

## 方案选型与排期

结合改造效果、稳定性保障与成本，**优先采用思路一 + 思路二并行实施**。

### 任务拆解

| 任务 | 工时 |
|------|------|
| Jira 申请新项目 | - |
| 搭建项目，迁移查询接口 | 1 day |
| 上游调用方接口切换 | 1 day |
| 上下游联调（SIM、UAT 环境测试） | 2 day |
| Buffer | 1 day |
