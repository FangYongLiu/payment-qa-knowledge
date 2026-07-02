---
id: tbl_marketorder_t_auto_recharge_task
object_type: Table
name: 自动充值任务表 (t_auto_recharge_task)
aliases: [t_auto_recharge_task, marketorder.t_auto_recharge_task]
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

# 自动充值任务表 (t_auto_recharge_task)

## 用途
物理表 `marketorder.t_auto_recharge_task`,主键 `id`。自动充值任务表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 |
| `config_id` | bigint(18) | 配置id |
| `batch_no` | bigint(18) | 批次号 |
| `order_no` | bigint(18) | 订单号 · 可空 |
| `member_id` | varchar(18) | 会员id |
| `target_no` | varchar(18) | 目标账号（加密字段） |
| `service_provider` | varchar(20) | 服务商 |
| `package_type` | varchar(20) | 套餐类型 |
| `goods_code` | varchar(20) | 商品code · 可空 |
| `sku_code` | varchar(20) | sku_code · 可空 |
| `amount` | decimal(10, 2) | 充值金额 · 可空 |
| `currency` | varchar(20) | 币种 |
| `task_status` | varchar(20) | 任务状态：WAIT（待处理），PROCESS（处理中），SUCCESS（处理成功），FAIL（处理失败） |
| `unity_result_code` | varchar(50) | 统一错误码 · 可空 |
| `fail_msg` | varchar(100) | 失败原因 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `account_type` | varchar(20) | 账户类型 · 可空 |
| `fail_type` | varchar(32) | 错误类型 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_config_id_batch_no`:config_id, batch_no (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
