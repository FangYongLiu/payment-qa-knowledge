---
id: tbl_acquireii_t_inst_code_config
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
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
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

存储**机构代码（inst_code）的全局配置**。`inst_code` 在多个订单类表中出现（如 `t_deposit_order.inst_code`、`t_preauth_control.inst_code`、`t_sharing_info.inst_code`），表示订单所属的金融机构或业务条线，是关键路由字段。

**典型场景**：
- 不同合作银行使用不同的 inst_code
- 不同业务类型（信用卡、借记卡、钱包）使用不同 inst_code
- 配置表存储 inst_code 的属性、规则、费率等

表名：`acquireii.t_inst_code_config`，重要程度 ⭐⭐⭐。

## 关键列

| 字段 | 类型 | 是否必填 | 说明 |
|------|------|---------|------|
| `id` | bigint | ✅ | 主键 |
| `inst_code` | varchar(32) | ✅ | 机构代码（唯一） |
| `inst_name` | varchar(200) |  | 机构名称 |
| `config_value` | varchar(2000) |  | 配置值（可能是 JSON） |
| `status` | varchar(32) |  | 配置状态（ACTIVE / DISABLED） |
| `created_time` | timestamp(3) | ✅ | 创建时间 |
| `last_updated_time` | timestamp(3) | ✅ | 最后更新时间 |

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | id | 主键 |
| `uk_icc_code` | inst_code | 唯一约束 |

被多个订单表通过 `inst_code` 字段引用（非强外键）：`t_deposit_order.inst_code`、`t_preauth_control.inst_code`、`t_sharing_info.inst_code`。

## 校验点(QA 关注)

1. **inst_code 是关键路由字段**：影响订单的处理逻辑，QA 需关注配置与订单流转的一致性。
2. **inst_code 唯一性**：由 `uk_icc_code` 保证，禁止重复。
3. **config_value 可能是 JSON**：使用前需要解析，注意格式与字段长度（varchar(2000)）。
4. **status 取值**：`ACTIVE` / `DISABLED`，仅 `ACTIVE` 用于生效配置。
5. **配置变更需谨慎**：变更可能影响正在交易的订单。
6. **建议加缓存**：高频访问场景下避免每次查 DB；QA 验证缓存刷新与一致性。
7. **常用查询**：
   - 按 inst_code 查配置：`SELECT * FROM t_inst_code_config WHERE inst_code = ?;`
   - 已启用列表：`SELECT inst_code, inst_name FROM t_inst_code_config WHERE status = 'ACTIVE' ORDER BY inst_code;`
