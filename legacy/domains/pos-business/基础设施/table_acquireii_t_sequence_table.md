---
id: tbl_acquireii_t_sequence_table
object_type: Table
domain: device-pos
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_sequence_table.md
tags:
- 序号生成
- 全局唯一
- 主键生成
subdomain: 基础设施
module: sequence
sensitivity: normal
name: 序号生成表
aliases:
- t_sequence_table
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_deposit_order
- tbl_acquireii_t_refund_order
- tbl_acquireii_t_request_identity
- tbl_acquireii_t_reversal_order
- tbl_acquireii_t_revoke_order
- tbl_acquireii_t_void_order
related_scenarios:
- scn_acquire_product_apply
- scn_merchant_transaction_db_check
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_sequence_table` 是收单(acquireII)体系的**全局唯一序号生成器**,替代 MySQL `auto_increment`,为订单号、退款号、撤销号、批次号等业务对象按业务前缀分组生成全局唯一序号。

**为什么不用 auto_increment**:
- 分库分表场景下 `auto_increment` 不能保证全局唯一。
- 需要按业务前缀分组生成(如订单号以 `AO` 开头、退款号以 `RO` 开头)。
- 需要带日期信息的序号(如 `YYYYMMDD + 序号`)。

**典型使用场景**:
- 创建收单订单(`t_acquire_order`)前:从 `sequence_name='ACQUIRE_ORDER'` 取下一个序号,拼接生成 `global_id`。
- 创建退款单(`t_refund_order`)、撤销单(`t_revoke_order` / `t_void_order`)、Reversal 单(`t_reversal_order`)、充值单(`t_deposit_order`)等同理,各使用各自的 `sequence_name`。
- 业务对象拼接成最终 `global_id`(业务前缀 + 日期 + 序号)。

## 在交易链路中的位置

该表位于交易链路的**最前端 ID 生成阶段**:

```
收单请求进入 → [t_sequence_table 取号] → 生成 global_id → 落库 t_acquire_order / t_refund_order / ... → 后续支付/对账流程
```

几乎所有写入主流程订单类表(收单、退款、撤销、Reversal、充值等)的链路,都会先访问本表取号。`t_request_identity` 用于幂等控制,与本表配合保证"同一笔业务请求最终只生成一个唯一 global_id"。

## 关键列

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `sequence_name` | varchar(64) | ✅ | 主键,序号名称(业务标识),如 `ACQUIRE_ORDER`、`REFUND_ORDER` |
| `current_value` | bigint | ✅ | 当前值 |
| `step` | int | ✅ | 步长(一次取多少) |
| `last_updated_time` | timestamp(3) | ✅ | 最后更新时间 |

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `sequence_name` | 主键 |

## 与关联表的关系

| 关联表 | 关系说明 | 使用的 sequence_name(示意) |
|--------|----------|------------------------------|
| `t_acquire_order` | 收单订单主表,创建前取号生成 `global_id` | `ACQUIRE_ORDER` |
| `t_refund_order` | 退款订单,创建前取号 | `REFUND_ORDER` |
| `t_revoke_order` / `t_void_order` | 冲正/撤销单,创建前取号 | `REVOKE_ORDER` / `VOID_ORDER` |
| `t_reversal_order` | Reversal 单,创建前取号 | `REVERSAL_ORDER` |
| `t_deposit_order` | 充值单,创建前取号 | `DEPOSIT_ORDER` |
| `t_request_identity` | 幂等表,与本表配合保证同一请求只取一次号 | - |

注:具体 `sequence_name` 命名以业务实际配置为准。

## 校验点(QA 关注)

1. **取号需 `SELECT ... FOR UPDATE` 加锁**:保证序号唯一性,避免并发取号产生重复。
2. **典型取号流程**:
   - `SELECT current_value, step FROM t_sequence_table WHERE sequence_name = 'ACQUIRE_ORDER' FOR UPDATE;`
   - `UPDATE t_sequence_table SET current_value = current_value + step, last_updated_time = NOW() WHERE sequence_name = 'ACQUIRE_ORDER';`
   - 应用层使用 `[old_value+1, old_value+step]` 这段序号。
3. **step 步长影响**:
   - 太小:频繁访问数据库,性能下降。
   - 太大:服务重启后浪费序号。
   - 常见值:100 ~ 1000。
4. **禁止直接修改 `current_value`**:除非确认序号不会重复,否则会引发主键冲突或重复业务号。
5. **不同 `sequence_name` 互不影响**:可同时存在订单序号、退款序号等多个序号空间。
6. **服务重启序号丢失**:应用层缓存(step 个)的内存中序号在重启后会丢失,重启后从 DB 取一段新序号即可,需关注业务号是否允许出现"跳号"。
7. **监控关注点**:通过 `last_updated_time` 监控哪些序号被频繁更新(对应高业务量),评估 step 是否合理。

## QA 落库检查要点

- **唯一性验证**:在压测/并发场景下检查 `t_acquire_order.global_id`、`t_refund_order.global_id` 等是否出现重复(本表设计要求绝对唯一)。
- **跳号容忍度**:确认业务方/对账方是否能接受重启导致的序号不连续(对账场景如 `t_stmt_event` 通常按 `global_id` 关联,不依赖连续性)。
- **前缀规则一致性**:验证生成的 `global_id` 业务前缀与 `sequence_name` 配置一致(如 `ACQUIRE_ORDER` 对应 `AO` 前缀)。
- **跨日期边界**:若序号包含日期段(`YYYYMMDD`),验证日切时序号是否按预期重置或衔接。
- **不要在用例中直接 UPDATE 该表**:测试用例如需重置序号,需评估是否会与现存订单 `global_id` 冲突。
