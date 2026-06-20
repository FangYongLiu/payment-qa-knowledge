---
title: PCBS Bin Sponsorship SFTP结构与权限设计
domain: ppc-card-business
kind: wiki_page
slug: pcbs-sftp-structure
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:18e736f3-6034-47a7-ae59-a59bc3bf2e5e
tags: []
---

# PCBS Bin Sponsorship SFTP结构与权限设计

本页说明 PCBS（Bin Sponsorship 服务）与外部合作伙伴（如 NymCard）之间共享 SFTP 的目录结构与权限分配方式，用于支撑文件交换驱动的业务处理。

## 角色与职责

- **NymCard Account（外部合作伙伴）**
  - 作为外部 Partner，将业务文件上传至共享 SFTP。
  - 上传的文件由我方服务读取后用于后续业务处理。
- **Business Service（pcbs，Bin Sponsorship 服务）**
  - 需要对**所有 Partner 目录**具备**读权限**。
  - 不负责上传，仅消费 Partner 上传的文件。

## SFTP 权限模型

- 每个 Partner 拥有自己的目录，仅能在其归属目录内上传文件。
- pcbs 服务需跨 Partner 目录读取，因此被授予所有 Partner 目录的读权限。
- 权限分配原则：
  - Partner：写入（上传）至自身目录。
  - pcbs：只读访问全部 Partner 目录。

## 文件处理约定

- Partner 上传文件后，由 pcbs 服务访问 SFTP 拉取并解析，进入 Bin Sponsorship 业务流程。
- 具体的 Partner 目录列表与账户配置以《Bin Sponsorship SFTP.xlsx》申请单为准。

## 参考资料

- PRD（需求文档）
- Bin Sponsorship SFTP.xlsx（Partner SFTP 账号与目录申请明细）
