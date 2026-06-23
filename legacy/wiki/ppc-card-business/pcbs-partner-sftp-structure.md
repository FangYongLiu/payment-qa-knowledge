---
title: PCBS Partner SFTP 结构与权限说明
domain: ppc-card-business
kind: wiki_page
slug: pcbs-partner-sftp-structure
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/813957140
tags: []
---

# PCBS Partner SFTP 结构与权限说明

本页描述 PCBS（Bin Sponsorship Service）与外部合作伙伴之间通过 SFTP 进行文件交换的目录使用方式、账号权限划分以及申请所需材料。

## 背景与用途

- PCBS（Bin Sponsorship Service）需要与外部合作伙伴通过 SFTP 交换业务文件。
- 当前涉及的外部合作伙伴：**NymCard**（见 PRD）。
- 文件由合作伙伴上传至 SFTP，由 PCBS 读取并进入后续业务处理流程。

## 账号与权限模型

涉及两类账号，权限分工如下：

- **Partner 账号（外部，例如 NymCard）**
  - 用途：将业务文件上传到该 partner 在 SFTP 上的目录。
  - 权限：对自身 partner 目录具备上传所需权限。
- **Business Service 账号（pcbs）**
  - 用途：读取各 partner 上传的文件，驱动 Bin Sponsorship 业务处理。
  - 权限：对**所有** partner 目录具备 **读权限**。

## 目录结构原则

- 按 partner 划分独立目录（每个外部合作伙伴一个文件夹）。
- Partner 仅操作自身目录；pcbs 跨所有 partner 目录读取。

## Partner SFTP 申请

申请 SFTP 资源时需提供的信息记录在附件中：

- 申请材料：`Bin Sponsorship SFTP.xlsx`
- 关联文档：PRD

申请时需明确：参与的 partner 列表、各 partner 账号、pcbs 服务账号，以及上述权限要求（partner 上传到自身目录、pcbs 读取所有 partner 目录）。
