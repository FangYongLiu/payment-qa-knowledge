---
id: ts_acquire_order_slow_sql
object_type: Troubleshooting
name: 收单订单查询慢SQL(t_acquire_order 大商户时间范围查询)
aliases: [acquire order slow sql, t_acquire_order 慢查询]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: wiki:cbd444e6 (收单订单查询慢SQL优化技术方案)
tags: [online-business, acquiring, slow-sql, performance, t_acquire_order]
related_services: [svc_acquireii, svc_acquire2_query]
related_tables: [tbl_acquireii_t_acquire_order, tbl_acquireii_t_payment_info, tbl_acquireii_t_secondary_merchant_detail]
related_logs: []
related_failures: []
---

# 收单订单查询慢SQL(t_acquire_order 大商户时间范围查询)

## 症状
商户 Portal 按时间范围查询收单信息,当**时间范围 > 1 个月**时出现慢查询;分页 count 统计耗时 >30s。

## 关联关系
- **涉及服务 / 表**:[[svc_acquireii]](收单)、[[svc_acquire2_query]](新建查询服务,走从库)/ [[tbl_acquireii_t_acquire_order]]、[[tbl_acquireii_t_payment_info]]、[[tbl_acquireii_t_secondary_merchant_detail]](= `related_services` / `related_tables`)。
- **相关日志**:`service:acquireii` 慢 SQL 日志(待补具体 index)。

## 可能根因
- 热点商户数据量巨大:`t_acquire_order` 全表 53,964,702 行,热点商户 `partner_id=200010278881` 占 **41,838,730 行(77%)**;命中该 partner_id + 大时间窗必然慢。
- 典型慢 SQL:`count(global_id)` 三表关联(`t_acquire_order` LEFT JOIN `t_secondary_merchant_detail` CROSS JOIN `t_payment_info`)+ `created_time` 范围 + `pay_channel='NYU_STUDENT_CARD'`,扫描行数 26,289,941。

## 排查步骤
- DB:确认查询 `partner_id` 是否为热点大商户;看 `created_time` 时间窗大小。
- 实测耗时基线(按窗口):2 周 2.94s(102 万行)/ 1 月 5.56s(190 万行)/ 2 月 12.02s(418 万行)。
- Kibana:看 acquireii 慢查询日志,关键字 partner_id / created_time。

## 处理 / 规避(落地方案 = 思路一 + 思路二)
- **思路一(约束时间范围)**:查询限 1 个月内,1 个月外数据归档 → 分页耗时 >30s 降至 ~10s;窗口越小越接近秒级。
- **思路二(新建查询服务走从库)**:[[svc_acquire2_query]] 独立查询服务读从库,避免非核心查询冲击主链路(收单服务 JPA 多数据源改造影响面大,不直接改主链路)。与思路一不冲突,可并行。
- 备选(未采纳):思路三(百万级以上结果集返回扫描行数作近似 count,省 ~5s,需业务可接受误差);思路四(热点 partner_id 独立分表,数据迁移+路由改造成本高)。
