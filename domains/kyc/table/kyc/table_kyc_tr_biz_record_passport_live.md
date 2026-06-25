---
id: tbl_kyc_tr_biz_record_passport_live
object_type: Table
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: DB DDL
source_ref: DataGrip DDL export (kyc schema) 2026-06-24
tags:
- kyc
- passport
- tr_biz_record_passport_live
subdomain: passport
module: null
sensitivity: restricted
name: 护照活体业务记录表(tr_biz_record_passport_live)
aliases:
- tr_biz_record_passport_live
related_services:
- svc_kyc
related_scenarios: []
---

# 护照活体业务记录表(tr_biz_record_passport_live)

## 用途
**护照活体业务记录**:护照 journey 的活体视频包解析与比对分数(`live_face_score`)。`record_id` 关联 tm_biz_record。对应 passport liveness/retake-selfie。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `req_token` | varchar(32) |  | kyc流程token |
| `record_id` | bigint(32) | NOT NULL | 业务记录ID |
| `req_image_package_tag` | varchar(70) |  | 用户提交的视频包 |
| `req_check_image_tag` | varchar(70) |  | 要比对的照片 |
| `live_channel_code` | varchar(32) |  | 通道编号 |
| `live_compare_file_tag` | varchar(32) |  | 活体认证取样照片 |
| `live_upload_file_list` | varchar(255) |  | 活体视频包解析的图片集合 |
| `live_face_score` | varchar(9) |  | 活体对比结果分数 |
| `resp_code` | varchar(15) |  | 响应编码 |
| `resp_msg` | varchar(255) |  | 响应详细 |
| `extension` | varchar(255) |  | 扩展字段 |
| `create_time` | timestamp | NOT NULL | 创建日期 |
| `update_time` | timestamp | NOT NULL | 更新日期 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_rid`:(`record_id`)

## 校验点(QA 关注)
- `live_face_score` 阈值;不达标触发重拍。
- 图片以 tag 引用不落原图。
