---
id: tbl_acquireii_t_retryable_command
object_type: Table
domain: acquire-payment-core
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_retryable_command.md
tags:
- retry
- command
- schedule
subdomain: command
module: null
sensitivity: normal
name: 可重试指令表
aliases:
- t_retryable_command
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
记录**可以被重试**的异步指令的重试调度信息。当指令执行失败时进入此表等待下次重试。

典型场景：
- 调用渠道接口超时 → 进入重试队列
- 商户回调失败 → 进入重试队列
- 网络抖动导致的临时失败

与 `t_command` 的区别：
- `t_command`：所有指令的主表
- `t_retryable_command`：指令的重试调度信息（下次重试时间、已重试次数等）

表名：`acquireii.t_retryable_command`，主键 `id`，重要程度 ⭐⭐⭐⭐。

## 关键列

主键和指令信息：
- `id` bigint ✅ 主键，对应 `t_command.id`
- `category` varchar(50) ✅ 指令类别
- `external_order_id` varchar(100) 外部订单 ID
- `status` varchar(32) 状态
- `memo` varchar(100) 备注

重试控制：
- `next_retry_time` timestamp(3) **下次重试时间**（调度关键字段）
- `retry_count` int 已重试次数
- `max_retry_count` int 最大重试次数

时间和版本：
- `created_time` timestamp(3) ✅ 创建时间
- `last_updated_time` timestamp(3) ✅ 最后更新时间
- `data_version` bigint ✅ 数据版本

## 主键/索引
- PRIMARY：`id`
- `i_rc_eoi`：`external_order_id`，按外部订单查
- `i_rc_nrt`：`next_retry_time`，**调度核心索引**

关联表：
- `t_command` 1:1，关联字段 `id`
- `t_command_param` 1:N，关联字段 `id`

## 校验点(QA 关注)
1. **重试策略由调度器控制**：通常用退避算法（指数级或固定）。
2. **next_retry_time 是调度关键字段**：调度器按此字段扫描；查询即将重试的指令使用 `next_retry_time <= NOW() AND status = 'PENDING'` 并按 `next_retry_time` 排序。
3. **达到 max_retry_count 不再重试**：`retry_count >= max_retry_count` 且 `status = 'FAILED'` 的需要人工介入/告警流程。
4. **慎重设置 max_retry_count**：太多浪费资源，太少业务损失。
5. **业务异常 vs 系统异常**：业务错误不应该重试（如金额超限）。
6. 排查某订单的重试历史可按 `external_order_id` 查询并按 `created_time` 排序。
