---
id: tbl_marketorder_t_auto_recharge_open
object_type: Table
name: 自动充值开通表 (t_auto_recharge_open)
aliases: [t_auto_recharge_open, marketorder.t_auto_recharge_open]
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

# 自动充值开通表 (t_auto_recharge_open)

## 用途
物理表 `marketorder.t_auto_recharge_open`,主键 `id`。自动充值开通表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 |
| `member_id` | varchar(18) | 会员id |
| `service_provider` | varchar(20) | 服务商 |
| `package_type` | varchar(20) | 套餐类型 |
| `nick_name` | varchar(120) | 账户昵称 · 可空 |
| `target_no` | varchar(18) | 目标账号（加密字段） |
| `goods_code` | varchar(20) | 商品code |
| `sku_code` | varchar(20) | sku_code |
| `amount` | decimal(10, 2) | 充值金额 · 可空 |
| `currency` | varchar(20) | 币种 |
| `open_status` | varchar(20) | 开通状态：PROCESS（开通中），SUCCESS开通成功，FAIL开通失败 |
| `pending_status` | varchar(40) | 开通待处理事项：PROTOCOL_SIGN(协议签约) AUTO_DEBIT_IDENTIFY_HINT(风控自动扣款事件核身) NONE(不需要处理) |
| `sign_status` | varchar(4) | 当次是否签约过协议：已经签约 Y，未签约 N |
| `auto_payment_day` | varchar(8) | 几号 |
| `platform_type` | varchar(15) | 终端类型 |
| `identify_result` | varchar(20) | 核身结果 · 可空 |
| `identify_ticket` | varchar(100) | 核身令牌 · 可空 |
| `return_method` | varchar(20) | 核身返回处理方式 · 可空 |
| `protocol_no` | varchar(35) |  签约自动充值协议的协议号 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `account_type` | varchar(20) | 账户类型 · 可空 |
| `partner_id` | varchar(32) | 平台ID · 可空 |
| `fail_msg` | varchar(100) | 开通失败原因 · 可空 |
| `operate_type` | varchar(10) | 操作类型：NEW=新增、UPDATE=更新 · 可空 |
| `open_source` | varchar(16) | 开通来源 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
