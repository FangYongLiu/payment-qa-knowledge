---
id: tbl_css_tb_settle_agreement
object_type: Table
name: tb_settle_agreement (tb_settle_agreement)
aliases: [tb_settle_agreement, css.tb_settle_agreement]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: css schema DDL
tags: [merchant-management, css]
sensitivity: normal
related_services: []
---

# tb_settle_agreement (tb_settle_agreement)

## 用途
物理表 `css.tb_settle_agreement`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键id · 可空 |
| `member_id` | varchar(32) | 会员id · 可空 |
| `biz_product_code` | varchar(18) | 产品码 · 可空 |
| `pay_channel` | varchar(12) | 支付渠道 · 可空 |
| `priority` | int(6) | 优先级(优先级的数字越大，优先级越高) |
| `status` | tinyint(2) | 状态 1:有效，0:无效 |
| `deal_type` | varchar(16) | 11:即时到账收单交易;14退款;15:合并支付;17:预授权交易;默认为空则表示16:交易 · 可空 |
| `settlement_cycle` | int | 结算周期，单位是分钟 |
| `settlement_type` | char | 结算类型：R-实时；T-时间触发；O：外部触发； |
| `execute_expression` | varchar(255) | 表达式 · 可空 |
| `cron_define` | varchar(255) | 结算周期corn表达式 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modify` | timestamp | 修改时间 |
| `gmt_effective` | timestamp | 生效时间 · 可空 |
| `gmt_invalid` | timestamp | 失效时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
