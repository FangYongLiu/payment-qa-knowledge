---
id: tbl_acquireii_t_sequence_table
object_type: Table
domain: pos-business
status: active
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
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_sequence_table` 是**全局唯一序号生成器**，替代 `auto_increment`，为订单号、退款号、批次号等业务对象按业务前缀分组生成唯一序号。

**为什么不用 auto_increment**：
- 分库分表场景下 `auto_increment` 不能保证全局唯一
- 需要按业务前缀分组生成（如订单号以 `AO` 开头）
- 需要带日期信息的序号（如 `YYYYMMDD + 序号`）

**典型场景**：
- 创建订单前：从 `sequence_name='ACQUIRE_ORDER'` 取下一个序号
- 创建退款：从 `sequence_name='REFUND_ORDER'` 取下一个序号
- 业务对象拼接成 `global_id`

## 关键列

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `sequence_name` | varchar(64) | ✅ | 主键，序号名称（业务标识），如 `ACQUIRE_ORDER`、`REFUND_ORDER` |
| `current_value` | bigint | ✅ | 当前值 |
| `step` | int | ✅ | 步长（一次取多少） |
| `last_updated_time` | timestamp(3) | ✅ | 最后更新时间 |

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `sequence_name` | 主键 |

## 校验点(QA 关注)

1. **取号需 `SELECT ... FOR UPDATE` 加锁**：保证序号唯一性，避免并发取号产生重复。
2. **典型取号流程**：
   - `SELECT current_value, step FROM t_sequence_table WHERE sequence_name = 'ACQUIRE_ORDER' FOR UPDATE;`
   - `UPDATE t_sequence_table SET current_value = current_value + step, last_updated_time = NOW() WHERE sequence_name = 'ACQUIRE_ORDER';`
   - 应用层使用 `[old_value+1, old_value+step]` 这段序号。
3. **step 步长影响**：
   - 太小：频繁访问数据库，性能下降。
   - 太大：服务重启后浪费序号。
   - 常见值：100 ~ 1000。
4. **禁止直接修改 `current_value`**：除非确认序号不会重复，否则会引发主键冲突或重复业务号。
5. **不同 `sequence_name` 互不影响**：可同时存在订单序号、退款序号等多个序号空间。
6. **服务重启序号丢失**：应用层缓存（step 个）的内存中序号在重启后会丢失，重启后从 DB 取一段新序号即可，需关注业务号是否允许出现"跳号"。
7. **监控关注点**：通过 `last_updated_time` 监控哪些序号被频繁更新（对应高业务量），评估 step 是否合理。
