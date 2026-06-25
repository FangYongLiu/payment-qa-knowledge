---
id: tbl_acquire_extension
object_type: Table
name: 收单扩展表(acquireii.t_acquire_extension)
aliases:
- t_acquire_extension
- acquireii.t_acquire_extension
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-25'
source_type: upload
source_ref: tables/t_acquire_extension.md
tags:
- extension
- 收单
related_services: [svc_acquireii]
related_scenarios: []
---

# 收单扩展表(acquireii.t_acquire_extension)

## 用途
`acquireii.t_acquire_extension` 是收单(acquireII)体系的**通用扩展信息存储表**，用于承载主表(收单订单 / 支付信息 / 指令等)无法在固定字段中表达的复杂业务数据，一般以 JSON 或自定义序列化字符串形式落库。重要程度 ⭐⭐(辅助类扩展表，非主链路核心表)。该表不直接参与交易主流程的状态推进，作为侧挂扩展存储，被主表通过 `extension_id`(global id)关联引用。

库表:`acquireii.t_acquire_extension`。补充场景:[[tbl_acquireii_t_acquire_order]] 的业务扩展属性、[[tbl_acquireii_t_payment_info]] 的渠道返回额外明细/风控字段、指令执行的透传上下文、金额明细的补充说明。

## 关联关系
- **所属服务**:[[svc_acquireii]](= frontmatter `related_services`,tbl→service 边)。
- **关键表**:[[tbl_acquireii_t_acquire_order]](通过 extension_id 关联，存放订单层扩展属性)、[[tbl_acquireii_t_payment_info]](支付信息扩展字段下沉);指令 `t_command`、金额明细 `t_amount_detail` 的扩展(对象待补)。关联方向是**主表 → 扩展表**，本表无反向外键。
- **哪些场景校验它**:商户交易落库检查等(对象待补)。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint ✅ | 主键，global id，跨业务统一生成 |
| `extension` | varchar(255) ✅ | 扩展数据(JSON / 序列化字符串)，长度上限 255 |
| `data_version` | bigint ✅ | 数据版本，乐观锁/版本控制 |
| `created_time` / `last_updated_time` | timestamp(3) ✅ | 创建/最后更新时间 |

## 主键 / 索引
- 主键:`id`(PRIMARY，仅支持按 id 精确查询)。

## 校验点(QA 关注)
- **extension 长度上限 255**:不能存大对象/长 JSON，写入前必须校验长度，避免被静默截断导致反序列化失败。
- **无固定 schema**:`extension` 内容格式由业务方约定，落库检查时需先确认该笔交易对应主表使用的格式再做内容比对。
- **data_version 一致性**:更新场景下关注版本号是否递增，防止并发覆盖。
- **id 为 global id**:跨业务共用同一张扩展表，id 必须由统一发号器生成，避免冲突。
- **落库检查链路**:主表存在 extension_id 时应反查本表确认扩展内容存在且格式正确，避免主表引用空 id 或脏数据。
- **清理与归档**:孤立的 extension 记录(无主表引用)属脏数据，需在巡检中关注。
