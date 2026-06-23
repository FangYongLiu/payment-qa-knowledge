---
title: UAT环境Maven settings.xml配置说明
domain: merchant-portal
kind: wiki_page
slug: uat-maven-settings-config
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:4121d0a7-aac9-49a6-95f6-609fd44283a8
tags: []
---

# UAT环境Maven settings.xml配置说明

本页说明 merchant-portal 业务域在 UAT 环境下使用的 Maven `settings.xml` 配置，包含部署服务器认证、仓库列表、插件仓库以及激活的 profile。

## 部署服务器认证（servers）

用于 `mvn deploy` 时向 Nexus 推送构件的账号配置：

- `deployRelease`：username=`dev`，password=`dev`
- `deploySnapshot`：username=`dev`，password=`dev`

server `id` 与下方 repository `id` 一一对应。

## 激活的 Profile

- `<activeProfiles>` 中激活 `development`，UAT 构建默认走该 profile 下的仓库列表。

## 依赖仓库（repositories）

profile `development` 下声明的依赖仓库，私服统一指向 `http://10.90.15.141:8181`：

| id | URL | releases | snapshots | 备注 |
| --- | --- | --- | --- | --- |
| `central` | `/content/groups/public` | enabled | enabled | 公共聚合组 |
| `internal` | `/content/groups/internal` | enabled，updatePolicy=`never` | enabled，updatePolicy=`always` | 内部聚合组 |
| `deployRelease` | `/content/repositories/releases/` | enabled | disabled | 与 server 同名，用于 release |
| `deploySnapshot` | `/content/repositories/snapshots/` | disabled | enabled | 与 server 同名，用于 snapshot |
| `releases2` | `/service/local/repositories/releases/content` | enabled，updatePolicy=`always` | enabled，updatePolicy=`always` | release 内容服务 |
| `releases3` | `/service/local/repositories/thirdparty/content` | enabled | enabled | 第三方构件 |
| `apache` | `https://repository.apache.org/content/repositories/releases/` | enabled | disabled | Apache 官方 |
| `maven` | `https://repo1.maven.org/maven2/` | enabled | enabled | Maven 中央 |
| `aspose` | `http://maven.aspose.com/repository/repo/` | enabled | enabled | Aspose 仓库 |

要点：

- `internal` 的 release 使用 `updatePolicy=never`，避免重复刷新已发布版本；snapshot 使用 `always` 以拿到最新快照。
- `deployRelease` / `deploySnapshot` 仓库分别只启用 release / snapshot，与发布通道严格区分。

## 插件仓库（pluginRepositories）

- `central`：`http://10.90.15.141:8181/content/groups/public`，releases/snapshots 均启用。
- `internal-plugin`：`http://10.90.15.141:8181/content/groups/internal`，releases `updatePolicy=never`，snapshots `updatePolicy=always`。

## 使用要点

- 私服地址、端口与账号均为 UAT 内部值，外网不可达；切换环境时需替换 `servers` 与所有 `repository`/`pluginRepository` 的 URL。
- 发布构件时 Maven 会按 `distributionManagement` 中的 `id` 匹配 `servers` 中同名条目获取认证。
- 如需调整刷新策略，重点关注 `internal` 与 `internal-plugin` 的 `updatePolicy`。
