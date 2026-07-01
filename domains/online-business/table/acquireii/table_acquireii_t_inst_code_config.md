---
id: tbl_acquireii_t_inst_code_config
object_type: Table
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_inst_code_config.md
tags:
- inst_code
- 机构配置
- 路由
subdomain: 配置
module: null
sensitivity: normal
name: 机构代码配置表
aliases:
- t_inst_code_config
- acquireii.t_inst_code_config
related_services:
- svc_acquireii
---

## 用途

`acquireii.t_inst_code_config`(机构代码配置表)存储**机构代码 `inst_code` 的全局配置**,是收单(acquireII)体系内的**关键路由配置表**。`inst_code` 在多个订单类表中作为非强外键引用,标识订单所属的金融机构、合作银行或业务条线,直接影响订单的处理逻辑、渠道路由与费率计算。

**典型使用场景**:
- 不同合作银行使用不同的 `inst_code` 区分清算路径
- 不同业务类型(信用卡 / 借记卡 / 钱包 / VAM 等)使用不同 `inst_code`
- 配置表存储 `inst_code` 的属性、规则、费率等元数据(可能以 JSON 形式存于 `config_value`)

表名:`acquireii.t_inst_code_config`,重要程度 ⭐⭐⭐。

## 在交易链路中的位置

该表属于**配置层 / 元数据层**,不直接参与交易流水写入,而是被订单与渠道处理模块**读取(常配缓存)**:

```
[请求进入] → 解析 inst_code → 查 t_inst_code_config(配置/状态/规则)
         ↓
[订单落库] t_acquire_order / t_deposit_order / t_preauth_control / t_sharing_info ... 写入 inst_code
         ↓
[渠道路由] 结合 t_channel_param / t_pay_scene_param 确定下游处理
```

## 关键列

| 字段 | 类型 | 是否必填 | 说明 |
|------|------|---------|------|
| `id` | bigint | ✅ | 主键 |
| `inst_code` | varchar(32) | ✅ | 机构代码(全局唯一) |
| `inst_name` | varchar(200) |  | 机构名称 |
| `config_value` | varchar(2000) |  | 配置值(可能为 JSON) |
| `status` | varchar(32) |  | 配置状态:`ACTIVE` / `DISABLED` |
| `created_time` | timestamp(3) | ✅ | 创建时间 |
| `last_updated_time` | timestamp(3) | ✅ | 最后更新时间 |

## 主键 / 索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | id | 主键 |
| `uk_icc_code` | inst_code | 唯一约束 |

## 与关联表的关系

被多个订单 / 业务表通过 `inst_code` 字段引用(**逻辑关联,非数据库强外键**):

| 关联表 | 引用字段 | 关系说明 |
|--------|---------|---------|
| `t_acquire_order` | `inst_code` | 收单主订单归属机构 |
| `t_deposit_order` | `inst_code` | 充值订单归属机构 |
| `t_preauth_control` | `inst_code` | 预授权控制按机构维度 |
| `t_sharing_info` | `inst_code` | 分账规则按机构区分 |
| `t_channel_param` / `t_pay_scene_param` | (常组合 inst_code) | 配合机构定位渠道与场景参数 |

## 校验点(QA 关注)

1. **inst_code 一致性**:订单表写入的 `inst_code` 必须能在 `t_inst_code_config` 中找到 `status='ACTIVE'` 的记录,否则路由 / 费率 / 分账可能出错。
2. **唯一性约束**:`uk_icc_code` 保证 `inst_code` 不重复,QA 在新增机构配置时需确认无冲突。
3. **`config_value` JSON 解析**:使用前需解析,关注字段长度上限 `varchar(2000)`,避免截断。
4. **`status` 取值**:仅 `ACTIVE` / `DISABLED`,只有 `ACTIVE` 才参与线上生效;DISABLED 后历史订单回查仍可读到记录。
5. **配置变更影响面**:变更可能影响正在交易的订单,QA 需在发布前评估在途订单与缓存刷新策略。
6. **缓存一致性**:高频访问场景通常加缓存,QA 需验证缓存 TTL、刷新机制与 DB 一致性(如更新后多久生效)。
7. **落库检查**:在商户交易落库检查类用例中,验证订单表中的 `inst_code` 与配置表中机构属性匹配(机构名、状态、业务类型等)。
8. **常用查询**:
   - 按 `inst_code` 查配置:`SELECT * FROM t_inst_code_config WHERE inst_code = ?;`
   - 已启用列表:`SELECT inst_code, inst_name FROM t_inst_code_config WHERE status = 'ACTIVE' ORDER BY inst_code;`
   - 反查订单使用某机构:`SELECT count(*) FROM t_acquire_order WHERE inst_code = ?;`
