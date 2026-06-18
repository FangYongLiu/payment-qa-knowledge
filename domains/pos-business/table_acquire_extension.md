---
id: tbl_acquire_extension
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_acquire_extension.md
tags:
- extension
- 收单
subdomain: null
module: null
sensitivity: normal
name: 收单扩展表
aliases:
- t_acquire_extension
- acquireii.t_acquire_extension
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_amount_detail
- tbl_acquireii_t_command
- tbl_acquireii_t_payment_info
related_scenarios:
- scn_merchant_transaction_db_check
related_logs: []
related_requirements: []
related_failures: []
---

## 用途与定位

`acquireii.t_acquire_extension` 是收单(acquireII)体系的**通用扩展信息存储表**，用于承载主表(如收单订单 / 支付信息 / 指令等)无法在固定字段中表达的复杂业务数据。一般以 **JSON 或自定义序列化字符串** 形式落库。

- 表名：`acquireii.t_acquire_extension`
- 表注释：extension
- 业务含义：收单扩展信息
- 重要程度：⭐⭐ (辅助类扩展表，非主链路核心表)

## 在交易链路中的位置

该表不直接参与交易主流程的状态推进，而是作为**侧挂扩展存储**，被主表通过 `extension_id`(global id) 关联引用，用于补充以下场景的数据：

- 收单订单 (`t_acquire_order`) 在标准字段之外的业务扩展属性；
- 支付信息 (`t_payment_info`) 中渠道返回的额外明细 / 风控字段；
- 指令 (`t_command`) 执行过程中需要透传的上下文参数；
- 金额明细 (`t_amount_detail`) 等附属信息的补充说明。

主表通常通过保存的 id (global id) 反查本表获取扩展内容。

## 关键列

| 字段 | 类型 | 是否必填 | 说明 |
|------|------|---------|------|
| `id` | bigint | ✅ | 主键，global id，跨业务统一生成 |
| `extension` | varchar(255) | ✅ | 扩展数据 (JSON / 序列化字符串)，长度上限 255 |
| `data_version` | bigint | ✅ | 数据版本，乐观锁/版本控制 |
| `created_time` | timestamp(3) | ✅ | 创建时间 |
| `last_updated_time` | timestamp(3) | ✅ | 最后更新时间 |

## 主键 / 索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | id | 主键，仅支持按 id 精确查询 |

## 常用查询

```sql
-- 通过主表(如 t_acquire_order / t_payment_info)拿到的 extension_id 反查
SELECT * FROM t_acquire_extension WHERE id = ?;
```

## 与关联表的关系

| 关联表 | 关系 | 说明 |
|--------|------|------|
| `t_acquire_order` | 1:1 / 1:N | 收单订单可通过 extension_id 关联本表，存放订单层扩展属性 |
| `t_payment_info` | 1:1 | 支付信息表的扩展字段下沉到本表 |
| `t_command` | 1:1 | 指令上下文中的扩展参数 |
| `t_amount_detail` | 1:1 | 金额明细的补充信息 |

注意：本表本身没有反向外键，关联方向是**主表 → 扩展表**。

## 校验点 (QA 关注)

1. **extension 长度上限 255**：不能存大对象/长 JSON，写入前必须校验长度，避免被静默截断导致反序列化失败。
2. **无固定 schema**：`extension` 内容格式由业务方约定 (JSON or 自定义分隔)，QA 在落库检查时需先确认该笔交易对应主表使用的格式，再做内容比对。
3. **data_version 一致性**：更新场景下需关注版本号是否递增，防止并发覆盖。
4. **id 为 global id**：跨业务场景共用同一张扩展表，id 必须由统一发号器生成，避免冲突。
5. **落库检查链路**：在【商户交易落库检查】等场景中，若主表存在 extension_id，应反查本表确认扩展内容存在且格式正确，避免出现主表引用了空 id 或脏数据的情况。
6. **清理与归档**：扩展数据生命周期需跟随主单据，孤立的 extension 记录(无主表引用)属于脏数据，需在巡检中关注。
