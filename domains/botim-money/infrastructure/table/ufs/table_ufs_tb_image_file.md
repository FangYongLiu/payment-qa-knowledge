---
id: tbl_ufs_tb_image_file
object_type: Table
name: 图片文件上传下载记录 (tb_image_file)
aliases: [tb_image_file, ufs.tb_image_file]
domain: infrastructure
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ufs schema DDL
tags: [infrastructure, ufs]
sensitivity: normal
related_services: []
---

# 图片文件上传下载记录 (tb_image_file)

## 用途
物理表 `ufs.tb_image_file`,主键 `file_id`。图片文件上传下载记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `file_id` | bigint | 文件ID · 可空 |
| `account_id` | int | 映射的Oss账户id · 可空 |
| `file_name` | varchar(255) | 包括路径的文件名 · 可空 |
| `is_temp` | int(1) | 文件是否是临时文件,0为永久,1为临时,缺省为0 |
| `expired_seconds` | bigint | 文件如果为临时文件,有效时间,以秒为单位.缺省为0秒 |
| `file_tag` | varchar(255) | 和oss文件对应的文件标志,用uuid生成 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |
| `application_name` | varchar(255) | 应用名,表明该文件是哪个业务应用调用ufs上传,下载文件接口的 |
| `extension` | varchar(255) | 扩展字段 |

## 主键 / 索引
- 主键:`file_id`
- `tb_file_data_tag_uindex`:file_tag (UNIQUE)
- `i_file_data_gmt_modified`:gmt_modified

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
