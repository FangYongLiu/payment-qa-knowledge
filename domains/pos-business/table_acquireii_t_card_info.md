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
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
记录**卡支付场景**下使用的卡详细信息，表名 `acquireii.t_card_info`，主键 `global_id`（对应订单 global_id），1:1 关联 `t_acquire_order`、`t_payment_info`。

包含内容：
- 卡号（脱敏存储）与掩码
- 卡组织（VISA / MASTERCARD / AMEX 等）
- 过期日期（年/月）
- 持卡人姓名
- 卡 Token（支付令牌化，用于后续免输卡号支付）
- 卡类型（CREDIT / DEBIT）/ 等级（PLATINUM / GOLD / STANDARD）
- 发卡行 / 发卡国家
- 访问类型 access_type（MANUAL / NFC / CHIP / SWIPE）

⚠️ **PCI DSS 敏感信息表**，权限严格控制；并非所有订单都有卡信息，仅卡支付场景产生。

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

⚠️ 表上仅有主键索引，**不要做带 `card_num` 的查询**（性能 + 安全），按 `global_id` 关联订单查询。

## 校验点(QA 关注)
1. **PCI DSS 敏感数据合规**：
   - `card_num` 不应被直接查询/展示；用户/日志展示必须使用 `card_num_mask`
   - 业务系统调用应使用 `card_token` 代替 `card_num`
2. **不是所有订单都有卡信息**：非卡支付场景该表无记录，关联查询用 LEFT JOIN
3. **brand 标准化**：可能存在大小写不一致，统计/匹配前需归一化
4. **card_token 过期校验**：使用前必须检查 `card_token_exp_time` 是否过期
5. **过期卡支付异常**：可通过 `CONCAT(exp_year, LPAD(exp_month,2,'0')) < 当前年月` 检出过期卡仍发生支付的异常
6. **access_type 风险等级**：NFC > CHIP > SWIPE > MANUAL，风险依次递增，需联动风控校验
7. **掩码字段一致性**：`card_num_mask` 与 `card_num_maskii` 需确认使用规则及数据一致性
8. **1:1 关系完整性**：与 `t_acquire_order` / `t_payment_info` 通过 `global_id` 一一对应，卡支付场景下不应缺失

</result>
