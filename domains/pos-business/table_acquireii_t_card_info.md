---
id: tbl_acquireii_t_card_info
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_card_info.md
tags:
- 敏感数据
- PCI-DSS
- 卡支付
subdomain: null
module: null
sensitivity: normal
name: 支付卡信息表
aliases:
- t_card_info
- acquireii.t_card_info
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_amount_detail
- tbl_acquireii_t_channel_param
- tbl_acquireii_t_command
- tbl_acquireii_t_dcc_info
- tbl_acquireii_t_fiserv_channel_param
- tbl_acquireii_t_pay_scene_param
- tbl_acquireii_t_payment_info
- tbl_acquireii_t_preauth_relation
- tbl_acquireii_t_promotion_info
related_scenarios:
- scn_acquire_product_apply
- scn_cko_standalone_card_binding
- scn_cko_subscription_test_cards
- scn_fiserv_test_tid_creation
- scn_merchant_transaction_db_check
- scn_mit_autodebit
- scn_mit_cit_directpay_first
- scn_mit_cit_directpay_subsequent
- scn_mit_cit_payandsign
- scn_mit_cit_test_guide
- scn_payment_code_scanned_by_pos
- scn_payment_code_scanned_by_scanner
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_card_info`（**支付卡信息表**）记录**卡支付场景**下使用的卡详细信息，主键 `global_id`（对应订单 global_id），与 `t_acquire_order`、`t_payment_info` 形成 **1:1 关联**。

包含内容：
- 卡号（脱敏存储）与掩码
- 卡组织（VISA / MASTERCARD / AMEX 等）
- 过期日期（年/月）
- 持卡人姓名
- 卡 Token（支付令牌化，用于后续免输卡号支付，支撑 MIT/CIT 场景）
- 卡类型（CREDIT / DEBIT）/ 等级（PLATINUM / GOLD / STANDARD）
- 发卡行 / 发卡国家
- 访问类型 access_type（MANUAL / NFC / CHIP / SWIPE）

⚠️ **PCI DSS 敏感信息表**，权限严格控制；并非所有订单都有卡信息，仅卡支付场景产生。

## 在收单交易链路中的位置

```
用户发起卡支付
   │
   ▼
t_acquire_order（订单主表，global_id 主键）
   │ 1:1
   ├──► t_payment_info（支付信息）
   ├──► t_card_info（本表，卡详情/Token）
   ├──► t_amount_detail（金额明细）
   ├──► t_dcc_info（如发生 DCC 货币转换）
   └──► t_preauth_relation（如为预授权场景）
```

- 上游：订单创建时根据请求中的卡信息/Token 落库本表。
- 下游：渠道指令（`t_command` / `t_command_param`）使用 `card_token` 或脱敏卡号下发到渠道（Fiserv/CKO/MPGS 等）。
- 关联渠道参数：`t_channel_param` / `t_fiserv_channel_param` 决定卡数据如何拼装下发。

## 关键列

**主键与卡基础**
- `global_id` bigint ✅ 主键，对应订单 global_id
- `brand` varchar(32) 卡组织（VISA / MASTERCARD / AMEX 等）
- `card_id` varchar(32) 卡 ID
- `card_num` varchar(32) 卡号（敏感）
- `card_num_mask` varchar(32) 卡号掩码（如 411111****1111）
- `card_num_maskii` varchar(32) 卡号掩码 v2
- `holder_name` varchar(32) 持卡人姓名

**过期日期**
- `exp_year` varchar(32) 过期年份
- `exp_month` varchar(32) 过期月份
- `card_expired_ues_token` varchar(32) 卡过期信息 token

**卡类型**
- `card_type` varchar(32) CREDIT / DEBIT 等
- `card_level` varchar(64) PLATINUM / GOLD / STANDARD 等

**发卡行**
- `issue_bank` varchar(32) 发卡行
- `issue_country` varchar(32) 发卡国家

**卡 Token**
- `card_token` varchar(64) 卡令牌
- `card_token_exp_time` timestamp(3) 卡令牌过期时间

**其他**
- `access_type` varchar(32) MANUAL / NFC / CHIP / SWIPE
- `created_time` timestamp(3) ✅ 创建时间

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | global_id | 主键 |

⚠️ 表上仅有主键索引，**不要做带 `card_num` 的查询**（性能 + 安全）。所有查询应通过 `global_id` 从 `t_acquire_order` 关联进入。

## 与关联表的关系

| 关联表 | 关系 | 关联键 | 说明 |
|--------|------|--------|------|
| `t_acquire_order` | 1:1（卡支付场景） | global_id | 订单主表，非卡支付场景下本表无记录，需 LEFT JOIN |
| `t_payment_info` | 1:1 | global_id | 支付信息（金额/状态/渠道），与本表配对 |
| `t_amount_detail` | 1:1 / 1:N | global_id | 金额拆分明细 |
| `t_dcc_info` | 0:1 | global_id | DCC 转币场景下卡币种信息联动 |
| `t_preauth_relation` | 0:N | global_id | 预授权场景下卡信息复用 |
| `t_pay_scene_param` | 0:1 | global_id | 支付场景参数（含 MIT/CIT 标识等） |
| `t_command` / `t_command_param` | 1:N | global_id | 渠道下发指令引用本表 card_token |
| `t_promotion_info` | 0:1 | global_id | 卡 BIN 优惠匹配可能依赖 brand/issue_bank |

## 校验点（QA 关注）

1. **PCI DSS 敏感数据合规**：
   - `card_num` 不应被直接查询/展示；用户/日志展示必须使用 `card_num_mask`
   - 业务系统调用应使用 `card_token` 代替 `card_num`
2. **不是所有订单都有卡信息**：非卡支付场景该表无记录，关联查询用 LEFT JOIN
3. **brand 标准化**：可能存在大小写不一致，统计/匹配前需归一化
4. **card_token 过期校验**：使用前必须检查 `card_token_exp_time` 是否过期；MIT/CIT 后续扣款若 token 过期会失败
5. **过期卡支付异常**：可通过 `CONCAT(exp_year, LPAD(exp_month,2,'0')) < 当前年月` 检出过期卡仍发生支付的异常
6. **access_type 风险等级**：NFC > CHIP > SWIPE > MANUAL，风险依次递增，需联动风控校验
7. **掩码字段一致性**：`card_num_mask` 与 `card_num_maskii` 需确认使用规则及数据一致性
8. **1:1 关系完整性**：与 `t_acquire_order` / `t_payment_info` 通过 `global_id` 一一对应，卡支付场景下不应缺失
9. **MIT/CIT 链路**：首次 CIT 落库 `card_token`，后续 MIT/CIT（DirectPay/PayAndSign/AutoDebit）应复用同一 token，校验 token 一致性与有效期
10. **POS/扫码场景**：付款码被扫场景下 `access_type` 与终端类型应匹配（POS 通常为 CHIP/NFC/SWIPE）
11. **发卡行/国家用于风控与费率**：`issue_bank` / `issue_country` 缺失会影响交叉境内外判断与 DCC 触发，需校验非空率

## 落库检查 SQL 模板

```sql
-- 基本卡信息（按 global_id 关联）
SELECT o.global_id, o.merchant_no, o.order_status,
       c.brand, c.card_num_mask, c.card_type, c.card_level,
       c.issue_country, c.access_type, c.card_token, c.card_token_exp_time
FROM acquireii.t_acquire_order o
LEFT JOIN acquireii.t_card_info c ON c.global_id = o.global_id
WHERE o.global_id = ?;

-- 过期卡仍支付异常
SELECT global_id FROM acquireii.t_card_info
WHERE CONCAT(exp_year, LPAD(exp_month,2,'0')) < DATE_FORMAT(NOW(),'%Y%m');
```
