---
id: tbl_merchant_t_fix_qr_code
object_type: Table
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (merchant schema) 2026-06-25
tags:
- merchant
- merchant
- t_fix_qr_code
subdomain: merchant
module: null
sensitivity: normal
name: 商户固码(t_fix_qr_code)
aliases:
- t_fix_qr_code
related_services:
- svc_merchant
related_scenarios: []
---
# 商户固码(t_fix_qr_code)

## 用途
商户固码。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | code id |
| `merchant_mid` | varchar(50) | NOT NULL | 商户mid |
| `store_id` | bigint | NOT NULL | 门店id |
| `store_name` | varchar(200) |  | 门店名称 |
| `name` | varchar(30) |  | 名称 |
| `code` | varchar(128) | NOT NULL | 编码 |
| `code_file_path` | varchar(128) |  | 固码文件路径 |
| `amount_type` | varchar(32) | NOT NULL | 金额类型 FIX 固定金额，CUSTOM 用户输入 |
| `fix_amount` | decimal(19,4) |  | 固定金额 |
| `currency_code` | varchar(20) |  | 币种 |
| `logo_path` | varchar(200) |  | logo图片路径 |
| `fix_qr_code_type` | varchar(10) | NOT NULL / 默认 'BOTIM' | fix qr code type |
| `status` | varchar(32) | NOT NULL | 状态 ENABLED 可用 INVALID 不可用 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `quick_input_tag` | varchar(32) |  | Quick input tag |
| `additional_fields_config` | varchar(255) |  | Save configuration for additional fields |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_fix_qr_code` 唯一 (code)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
