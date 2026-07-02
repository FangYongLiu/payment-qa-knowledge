---
id: tbl_acquireii_t_retryable_command
object_type: Table
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
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
related_services:
- svc_acquireii
---

## 表定位

表名：`acquireii.t_retryable_command`，主键 `id`，重要程度 ⭐⭐⭐⭐。

记录**可以被重试**的异步指令的重试调度信息。当指令执行失败、且失败原因属于可恢复类异常时，进入此表等待下次重试。

典型触发场景：
- 调用渠道接口超时 → 进入重试队列
- 商户回调（notify）失败 → 进入重试队列
- 网络抖动 / 渠道临时不可用导致的瞬时失败

## 在交易链路中的位置

收单链路中的异步指令统一由 `t_command` 编排：
- `t_command`：所有异步指令的主表（指令身份、上下文）
- `t_command_param`：指令的参数明细（1:N，按 `id` 关联）
- `t_retryable_command`：**可重试指令的调度信息**（下次重试时间、已重试次数等），由调度器轮询驱动
- `t_unretryable_command`：不可重试指令（业务级失败，例如金额超限、参数非法），不进入重试，等待人工或运营处理

失败分流原则：**系统/瞬时异常 → retryable**；**业务异常 → unretryable**。

## 关键列

主键和指令信息：
- `id` bigint ✅ 主键，对应 `t_command.id`（1:1）
- `category` varchar(50) ✅ 指令类别
- `external_order_id` varchar(100) 外部订单 ID（可关联 `t_acquire_order` 等业务订单）
- `status` varchar(32) 状态（典型值：`PENDING` 待重试、`FAILED` 终态失败）
- `memo` varchar(100) 备注（常用于记录最近一次失败原因）

重试控制：
- `next_retry_time` timestamp(3) **下次重试时间**（调度核心字段）
- `retry_count` int 已重试次数
- `max_retry_count` int 最大重试次数

时间和版本：
- `created_time` timestamp(3) ✅ 创建时间
- `last_updated_time` timestamp(3) ✅ 最后更新时间
- `data_version` bigint ✅ 数据版本（乐观锁）

## 主键 / 索引
- PRIMARY：`id`
- `i_rc_eoi`：`external_order_id`，按外部订单查重试历史
- `i_rc_nrt`：`next_retry_time`，**调度核心索引**

## 关联关系
- `t_command` 1:1，关联字段 `id`
- `t_command_param` 1:N，关联字段 `id`
- 通过 `external_order_id` 间接关联 `t_acquire_order`、`t_refund_order`、`t_void_order` 等业务订单
- 与 `t_unretryable_command` 是**互斥关系**：同一指令只会落到其中一张表

## QA 落库检查要点

1. **重试策略由调度器控制**：通常用退避算法（指数级或固定间隔）。验证 `next_retry_time` 的递推是否符合配置的退避曲线。
2. **next_retry_time 是调度关键字段**：调度器按此字段扫描，查询即将重试的指令使用 `next_retry_time <= NOW() AND status = 'PENDING'` 并按 `next_retry_time` 排序。
3. **达到上限不再重试**：`retry_count >= max_retry_count` 且 `status = 'FAILED'` 的记录需要人工介入/告警，QA 测试覆盖最大重试次数边界。
4. **max_retry_count 配置合理性**：太多浪费资源，太少业务损失；不同 `category` 可能配置不同上限。
5. **业务异常 vs 系统异常**：业务错误（金额超限、签名错误等）不应进入本表，应去 `t_unretryable_command`。QA 需通过 mock 不同失败码验证分流是否正确。
6. **重试成功后的清理 / 终态**：成功后 `t_command` 状态推进为成功态，本表记录通常停止调度（status 切换或被清理），需确认是否会出现僵尸记录。
7. **排查某订单的重试历史**：按 `external_order_id` 查询本表并按 `created_time` 排序，结合 `t_command_param` 还原参数。
8. **幂等性**：每次重试调用渠道时必须保证幂等（依赖 `t_request_identity` 等），避免重复扣款 / 重复通知。
9. **data_version 乐观锁**：调度器在更新 `next_retry_time` / `retry_count` 时应使用乐观锁，防止并发重试。