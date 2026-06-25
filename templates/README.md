# 知识文档编写规范(上传 / 新建文档前必读)

> 目标:**有血肉 + 全连边**。每个文档按模板写够内容(血肉),并且**每新增一个对象,
> 都回头更新所有相关对象的关联信息**(连边)。只有这样,reindex 出来的知识图谱才是系统的真实镜像。

---

## 0. 两条铁律
1. **按模板写**:每类对象用 `templates/<类型>.md` 的 frontmatter + 正文小节,一节不少。
2. **新增即回写**:新建任何一个 `.md`,必须按 §4 的清单更新**其它已存在文档**的关联信息——
   不是只写自己,而是把自己织进网里。漏回写 = 有叶子无主干。

不确定 / 查不到的内容:统一标 **「待补」**,不要臆造。标了待补,检索时能发现,人工再补充更新。

---

## 1. 八类对象 + 命名
| 类型 | id 前缀 | 文件名 | 何时用 |
| --- | --- | --- | --- |
| Service | `svc_` | `service_<app_group>_<name>.md` | 一个可部署服务/应用 |
| API | `api_` | `api_<service>_<name>.md` | 一个接口 |
| Table | `tbl_` | `tbl_<schema>_<table>.md` | 一张库表 |
| Scenario | `scn_` | `scn_<域>_<name>.md` | 一个业务测试场景 |
| Flow | `flow_` | `flow_<name>.md` | 一条端到端流程 |
| Troubleshooting | `ts_` | `ts_<symptom>.md` | 一个排障/故障案例 |
| AutomationAsset | `auto_` | `auto_<域>_<name>.md` | 一套自动化资产(测试套件) |
| Domain | `domain_` | `domain_<slug>.md` | 一个业务域总览 |

**文件名带 `app_group`**(服务),其它对象文件名带所属域/服务,风格统一。

---

## 2. Frontmatter(机器读:身份 + 图边 + 治理)
- `id` 唯一、前缀正确;**改文件名不改 id**(reindex 按 id 重建,改名对图谱透明)。
- `owner` / `reviewer`:**知识负责人,按 12 业务域映射**(见 `index/domains.yaml`),≠ `dev_owner`(开发联系人)。
- `status: active` 才进生产检索;`domain` 必填(未认领填 `service-catalog`)。
- `app_group` / `layer`:Service 专有;其它类型不用。
- **`related_*` 就是图的边**(见 §3)。

---

## 3. 关系模型(连边的机制,务必理解)
**只有这 6 个 frontmatter 字段会生成图边**:

| 字段 | 边 | 指向 |
| --- | --- | --- |
| `related_services` | uses_service | 服务 |
| `related_tables` | reads_table | 表 |
| `related_scenarios` | covered_by_scenario | 场景 |
| `related_failures` | has_failure | 故障 |
| `related_logs` | logged_in | 日志(伪节点) |
| `related_requirements` | impacts_requirement | 需求(伪节点) |

要点:
- **正文里的 `[[链接]]`,在 typed 对象中不生成边**(只有 wiki 页的 `[[]]` 生成 `references` 边)。
  正文 `[[]]` 是给人看/导航;真正的边在 frontmatter `related_*`。
- **单边声明**:每条边只从"自然源头"声明一次,不双向重复(否则重复边 + 维护漂移)。
  `impact_analysis` 走**双向遍历**,单边声明两头都能查到。
- **没有 `related_apis` 字段**:服务↔API 的边由 **API 的 `related_services`** 提供(api→svc)。
- **不要指向不存在的对象**(会产生悬空边)。对象还没建时,在正文写名字 + 标「待补」,别硬连。

### 边归属矩阵(谁声明什么)
| 对象 | 自己声明的 related_* |
| --- | --- |
| Service | services(下游)/ tables / scenarios |
| API | services(所属)/ tables / scenarios |
| Table | services(所属)/ scenarios |
| Scenario | services / tables / logs |
| Flow | services / tables / scenarios |
| Troubleshooting | services / tables / logs / failures |
| Domain | services(关键服务) |
| AutomationAsset | scenarios / services |

---

## 4. ★ 新增对象时的回写清单(全连边的核心)
新建一个对象后,**按下表回头更新相关文档**(frontmatter 边 + 正文 `[[链接]]` 都要):

- **新增 Service**
  - `domain_<域>.md` 的「关联关系」加 `[[svc_x]]`(并把它写进 `related_services`)
  - 它的上下游服务:由**调用方**在 `related_services` 声明
- **新增 API**
  - 所属 `service_*.md` 正文「涉及的 API / 数据库表」加 `[[api_x]]`
  - `api_x.related_services = [svc]`;已知则补 `related_tables` / `related_scenarios`
- **新增 Table**
  - 所属 `service_*.md` 正文「涉及的…表」加 `[[tbl_x]]`
  - 读写它的 Service / API:在各自 `related_tables` 加 `tbl_x`
- **新增 Scenario**
  - `scn_x.related_services` / `related_tables`
  - 被它测的每个 `api_*.md`:`related_scenarios` 加 `scn_x` + 正文「被哪些场景测」加 `[[scn_x]]`
  - 覆盖它的 `auto_*.md`:`related_scenarios` 加 `scn_x`
- **新增 AutomationAsset**
  - `auto_x.related_scenarios`(覆盖的场景)/ `related_services`(跑在/针对的服务)
  - 它调用的每个 `api_*.md`:正文「被哪些自动化覆盖」加 `[[auto_x]]`
  - 它覆盖的每个 `scn_*.md`:正文「覆盖它的自动化」加 `[[auto_x]]`
  - 所属 `service_*.md` / `domain_*.md` 正文加 `[[auto_x]]`
- **新增 Domain**
  - `related_services` = 该域关键服务;「关联关系」列关键服务 / 流程 / 自动化

> 经验法则:**任何 A→B 的关系,A 和 B 两个文档都要能看到对方**(一边靠 frontmatter 边,另一边靠正文链接 + 反向边)。

---

## 5. 完整样板:kyc 域
kyc 是第一个"有血肉 + 全连边 + 全数据源"的样板域,结构与做法可照搬:

```
domain_kyc (1)  ← 总览:概述/3渠道/覆盖范围/关联关系/QA关注点(含已知坑)/环境接入
  ├─ service_gp078_kyc / service_gp202_kyc_service (2)
  ├─ api_kyc_* (33)            ← API 文档(路径/入参/出参/错误码/校验点)
  ├─ table_kyc_* (36)          ← member/kyc 库 DDL 解析建表 + 连边
  ├─ scn_kyc_* (5)             ← cgs-apitest 用例按业务流归并
  ├─ flow_kyc_* (3)            ← 端到端流程(护照/续期/换绑,nextStep 状态机/渲染规则)
  ├─ auto_kyc_* (2)            ← cgs-apitest 测试套件
  └─ ts_kyc_* (4)              ← Kibana 错误日志挖的"已知坑"
```
连边:domain→service/flow、api→service、scn/flow/ts/auto→service、api↔scn、tbl→service、api→tbl;
正文交叉链接 + 反向小节让两头都能看见对方。

### 整理一个域 / 一批文档的完整流程(可复用 playbook)
按**数据源**分 pass,缺哪块补哪块。每个 pass 都遵守 §2–§4(模板 + 连边 + 回写)。

1. **骨架与归域**:服务对象先建/归域(`import_services.py`);`dev_owner` 用英文 `Given.Surname`,
   `owner`=域 lead(见 `index/domains.yaml`);**文件按 `domains/<域>/` 存放,`domain` 字段必须==目录**。
   归域以 dev/团队为主、保护业务域(kyc/card/remittance/compliance/risk 不被搬出);拿不准留 `service-catalog`。
2. **上下游边(callgraph)**:用 **PayBy-service-callgraph** skill 在 UAT Kibana 挖 `*ClientImpl` 聚合
   (类名词干=被调方)→ 真实 `related_services` 边 + 频次。⚠️ `app_id` 是日志里的部署名(如 kyc,**不是 gp078**)。
   下游=本服务发出的 `*ClientImpl`;上游=别人发出的 `*<本服务>ClientImpl`。
3. **表结构(Table 层)**:拿该库 **schema DDL** → 脚本解析建 `tbl_<schema>_<table>`
   (列/类型/PK/索引/注释来自 DDL=确定性;用途/校验点/subdomain/sensitivity 人工策展)→
   **回填**引用方的 `related_tables`(把"待补"文字变真边)。**DDL 没给的表不臆造**。
4. **已知坑(Troubleshooting)**:Kibana 按 `app_id` 聚合 `mLevel=ERROR/WARN` by `mClass.keyword` → 读高频原文 → 建 `ts_`。
   **区分业务错误 vs 基础设施噪声**(PingConnectionHandler/ClusterConnectionManager/ConfigServerHealthIndicator);
   诚实标"频次含 UAT 测试数据噪声,真坑 vs 噪声需人工确认";**预期行为不建坑**。
5. **正向业务信息(关键方法)**:Kibana 按 `app_id` 聚合 `mLevel=INFO` by `mClass` → 业务 Processor/Handler/Facade 类
   = 实际跑的业务操作 → 写进服务「关键方法/入口」;剔除 infra 类(SegmentIDGen/Compensation*/Zookeeper)。
6. **场景/自动化(cgs-apitest)**:读 `cgs-apitest/testcases/**/test_*.py` → 按业务流**归并**成 Scenario(非 1:1,排除夹具)
   + 每套件一个 AutomationAsset(TC 列表取自 `allure.title`/函数名);`related_services` 连穿过的服务(含跨域,反向边丰富核心域)。
7. **端到端流程(Flow)**:把流程类知识(跨系统时序、状态机/`nextStep`、页面渲染规则)建成 `flow_`。
8. **legacy/归档整合**:逐篇读懂→判定(已被现域覆盖=直接删 / 有新价值=建少数高质量对象,**合并非 1:1**)→删原文。
   大规模用**多智能体 workflow 按主题簇并行**;agent **只「新建+删除」、禁改已有文件**(防并发冲突);
   `related_*` 只连 grep 确认存在的对象;主循环事后统一做**反向链接回写**(给现有 service/domain 加 `[[新对象]]`)。
9. **不确定的一律标「待补」**,不臆造(表/字段/失败分支/下游对象缺失等)。

### ⚠️ enum / 格式硬约束(违反则 reindex **静默跳过**该对象,或整批中断)
- `sensitivity` 只能 **`normal` / `restricted`**(不是 `sensitive`!)。
- `object_type` 只能 **9 类**:Domain / Service / API / Table / Flow / Scenario / Troubleshooting / AutomationAsset / **Reference**(参考/字典页)。
- `tags` 必须**全是字符串**:纯数字(如 `707`)要加引号 `'707'`,否则被 YAML 当 int → 校验失败。
- `related_*` 用流式 `[a, b]` **或**块式 `- a` 之一,**不能混用**(混用 YAML 解析报错 → 整个 reindex 中断)。

### 上线(reindex)
- **改了 brain 代码**(如 enum):先重建镜像 `cd infra && docker compose --profile api --profile worker build api worker && docker compose --profile api --profile worker up -d api worker`(容器是烘焙镜像,非挂载);**纯数据(.md)改动不用重建**。
- 触发 `POST /api/brain/reindex` body `{"scope":"all"}`(token 在 brain `.env` `BRAIN_SERVICE_TOKEN`);轮询 `GET /api/brain/reindex/status`。
- 验证:运行时 DB 各域对象数、`errors=[]`、运行时 Table/对象数 ≈ 仓库数(差额说明有对象被跳过 → 查 enum/YAML/dup)。

---

## 6. 提交前自检
- 每个新文档:frontmatter 字段齐全、正文小节齐全(对照 `templates/<类型>.md`)。
- `related_*` 不指向不存在的对象(**零悬空边**;grep 确认每个 id 存在)。
- **零重复 id**(并行生成/多源易撞,`grep -rh '^id:' domains/ | sort | uniq -d`)。
- **enum 合法**(§5 硬约束):`sensitivity` ∈ {normal,restricted};`object_type` ∈ 9 类;`tags` 全字符串;`related_*` 不混流式/块式。
- **YAML 合法**:每个 frontmatter 能 `yaml.safe_load`(可用 brain `.venv/bin/python` 批量校验)。
- 回写清单(§4)都做了——新对象在相关文档里都能被看到(含反向小节)。
- 不确定的都标了「待补」,没有臆造(尤其 DDL 未提供的表、缺失的下游对象)。
- reindex 后:`errors=[]` 且运行时对象数 ≈ 仓库对象数(差额=被静默跳过,回查上面各项)。
