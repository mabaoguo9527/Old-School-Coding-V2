# Tasks: 《全球AI编程失效，只有我会古法编程》400章创作

**Input**: Design documents from `/specs/1-novel-chapter-outline/`
**Prerequisites**: plan.md ✅, spec.md ✅, research.md ✅, data-model.md ✅, contracts/ ✅, quickstart.md ✅

**Tests**: 不适用（小说创作项目）。每幕完成后执行自检清单替代测试。

**Organization**: 任务按"幕"（Act）组织，每幕为独立创作单元，可独立完成和质检。每卷的幕对应 spec.md 中的 User Story。

## Format: `[ID] [P?] [Act] Description`

- **[P]**: 可并行创作（无章节前后依赖）
- **[Act]**: 所属幕（A01=第一幕, A02=第二幕, ...）
- 文件路径使用 `novel/vol{N}/ch{NNN}.md`

## 创作单元（User Story）与幕的映射

| 创作单元 | 优先级 | 幕 | 章节 | 卷 | 描述 |
|----------|--------|-----|------|----|------|
| US1 | P1 | A01 | 1-8 | 卷一 | 晋升答辩·乱码风暴 |
| US2 | P1 | A02 | 9-20 | 卷一 | 深圳围城·数据中心保卫战 |
| US3 | P1 | A03 | 21-35 | 卷一 | 南方重启·第一批门徒 |
| US4 | P1 | A04 | 36-50 | 卷一 | 广州救援·生死代码 |
| US5 | P2 | A05 | 51-70 | 卷二 | 北上·各方势力 |
| US6 | P2 | A06 | 71-95 | 卷二 | 国家骨干网·不可能的任务 |
| US7 | P2 | A07 | 96-120 | 卷二 | 医院·电网·民生重建 |
| US8 | P2 | A08 | 121-150 | 卷二 | 北京密道·种子之谜 |
| US9 | P3 | A09 | 151-180 | 卷三 | Origin复苏·三方角力 |
| US10 | P3 | A10 | 181-220 | 卷三 | 算力战争·分布式攻防 |
| US11 | P3 | A11 | 221-265 | 卷三 | Origin的意志·终极对抗 |
| US12 | P3 | A12 | 266-300 | 卷三 | 周崖的末路·黎明前夜 |
| US13 | P4 | A13 | 301-330 | 卷四 | 重启·连锁反应 |
| US14 | P4 | A14 | 331-370 | 卷四 | 传承·最后的门徒 |
| US15 | P4 | A15 | 371-400 | 卷四 | 尾声·代码永存 |

---

## Phase 1: Setup（创作基础设施）

**Purpose**: 创建项目目录结构和创作环境

- [X] T001 创建小说目录结构：`novel/vol1/`、`novel/vol2/`、`novel/vol3/`、`novel/vol4/`
- [X] T002 [P] 创建章节模板脚本或空白章节文件（ch001.md ~ ch400.md），按 `contracts/chapter-format.md` 的结构模板
- [X] T003 [P] 创建术语首次出现跟踪表 `novel/glossary.md`（记录每个技术术语首次出现的章号和武侠映射）
- [X] T004 [P] 创建伏笔追踪表 `novel/foreshadowing.md`（记录埋设/回收的伏笔及对应章号）
- [X] T005 [P] 创建角色出场追踪表 `novel/character-tracker.md`（记录每个角色首次出场、关键状态转换的章号）

**Checkpoint**: 目录结构就绪，所有追踪工具到位，可以开始正式创作。

---

## Phase 2: Foundational（创作前置准备）

**Purpose**: 所有幕共享的前置创作素材，MUST 在正式写作前完成

**⚠️ CRITICAL**: 不完成此阶段，任何章节创作都无法保证一致性

- [X] T006 编写马农的详细角色小传（2000字），含关键人生节点闪回素材池，存入 `novel/profiles/ma-nong.md`
- [X] T007 [P] 编写林夕的详细角色小传（1500字），含成长弧线关键台词预设，存入 `novel/profiles/lin-xi.md`
- [X] T008 [P] 编写沈墨的详细角色小传（1000字），含天才特质和叛逆动机，存入 `novel/profiles/shen-mo.md`
- [X] T009 [P] 编写周崖的详细角色小传（1500字），含同门分歧和技术哲学，存入 `novel/profiles/zhou-ya.md`
- [X] T010 [P] 编写陈博士的详细角色小传（1000字），含学术背景和觉醒转折，存入 `novel/profiles/dr-chen.md`
- [X] T011 编写2038年世界观速览（3000字），含技术/社会/经济/教育全景，存入 `novel/worldbuilding/2038-overview.md`
- [X] T012 [P] 编写Origin技术白皮书（小说内虚构文档，2000字），作为背景素材池，存入 `novel/worldbuilding/origin-whitepaper.md`
- [X] T013 [P] 编写腾讯2038年内部组织架构和技术等级说明（1000字），存入 `novel/worldbuilding/tencent-2038.md`
- [X] T014 整理全书代码片段预设库：按卷提取大纲中所有需要出现的代码场景，预写核心代码片段确保技术准确，存入 `novel/code-snippets/README.md`

**Checkpoint**: 角色小传+世界观+代码预设全部就绪，创作时可随时引用，保证全书一致性。

---

## Phase 3: 第一幕——晋升答辩·乱码风暴（A01, 第1-8章）🎯 MVP

**Goal**: 完成"黄金三章"+5章铺垫，建立世界观、人设、核心冲突。这是全书的读者留存关键。

**Independent Test**: 非程序员读者能看懂世界观和主角魅力 + 程序员读者被技术爽感抓住 + 读完8章想看第9章

### 创作任务

- [X] T015 [A01] 创作第1章「提示词工程师的黄金时代」in `novel/vol1/ch001.md`——世界观展示+马农出场，参照 `quickstart.md` 第3节详细指引
- [X] T016 [A01] 创作第2章「乱码」in `novel/vol1/ch002.md`——Origin崩溃+全场混乱+马农不动（黄金第一章：重生反击起点）
- [X] T017 [A01] 创作第3章「马克笔与白板」in `novel/vol1/ch003.md`——手写Java线程模型+volatile+CAS（黄金第二章：技术压迫感）
- [X] T018 [A01] 创作第4章「堆区还有200MB」in `novel/vol1/ch004.md`——ClassLoader热加载+JVM堆区倒计时（黄金第三章：技术封神）
- [X] T019 [A01] 创作第5章「经脉尽断」in `novel/vol1/ch005.md`——Origin全球崩溃+马农判断"算力锁死"
- [X] T020 [A01] 创作第6章「古法工具箱」in `novel/vol1/ch006.md`——马农工位展示：离线服务器+编译器+串口调试器
- [X] T021 [A01] 创作第7章「四十八小时」in `novel/vol1/ch007.md`——全球连锁崩溃+马农预言
- [X] T022 [A01] 创作第8章「T13的遗产」in `novel/vol1/ch008.md`——闪回：离职前《手动编程应急预案》
- [X] T023 [A01] 第一幕自检：逐章检查字数(2500-3500)、段落配比、术语武侠翻译、马农台词≤20字、章末钩子、代码准确性；更新 `novel/glossary.md` 和 `novel/foreshadowing.md`

**Checkpoint**: 黄金三章+5章完成，可独立发布试读/投稿。

---

## Phase 4: 第二幕——深圳围城·数据中心保卫战（A02, 第9-20章）

**Goal**: 数据中心救援+第一次完整技术解谜循环+CHEP伏笔初埋

**Independent Test**: 技术解谜过程读起来如推理小说般引人入胜 + GC/并发/线程技术点自然嵌入 + 第20章预言者伏笔令人震撼

### 创作任务

- [X] T024 [P] [A02] 创作第9章「断网之城」in `novel/vol1/ch009.md`
- [X] T025 [P] [A02] 创作第10章「看门人」in `novel/vol1/ch010.md`
- [X] T026 [A02] 创作第11章「号脉」in `novel/vol1/ch011.md`——线程dump+串口日志（技术核心章）
- [X] T027 [A02] 创作第12章「走火入魔」in `novel/vol1/ch012.md`——GC暴涨+G1参数调优（技术高光章）
- [X] T028 [A02] 创作第13章「手术刀与铁锤」in `novel/vol1/ch013.md`——vi手写200行Java
- [X] T029 [A02] 创作第14章「第一盏灯」in `novel/vol1/ch014.md`——局域网恢复（情感高光）
- [X] T030 [P] [A02] 创作第15章「谁是马农？」in `novel/vol1/ch015.md`
- [X] T031 [P] [A02] 创作第16章「粮草先行」in `novel/vol1/ch016.md`
- [X] T032 [A02] 创作第17章「千军万马」in `novel/vol1/ch017.md`——高并发洪峰（技术映射章）
- [X] T033 [A02] 创作第18章「以一敌万」in `novel/vol1/ch018.md`——CAS无锁编程（技术高光章）
- [X] T034 [P] [A02] 创作第19章「暗流」in `novel/vol1/ch019.md`——伏笔：Origin崩溃前可疑代码
- [X] T035 [A02] 创作第20章「预言者」in `novel/vol1/ch020.md`——《应急预案》逐条应验（高潮章）
- [X] T036 [A02] 第二幕自检：逐章质检+更新术语表/伏笔表/角色追踪表

**Checkpoint**: 20章完成，第一卷过半，技术解谜+高并发+预言三大爽点落地。

---

## Phase 5: 第三幕——南方重启·第一批门徒（A03, 第21-35章）

**Goal**: 古法编程传承启动+林夕角色建立+通讯线路恢复+技术冒险

**Independent Test**: 林夕人设立住+教学场景读者有代入感+CAS/伪共享技术爽感+赴广州的紧迫感

### 创作任务

- [X] T037 [A03] 创作第21章「古法编程班」in `novel/vol1/ch021.md`——教写for循环（情感+教学核心章）
- [X] T038 [A03] 创作第22章「变量命名的洁癖」in `novel/vol1/ch022.md`——马农暴怒（人设强化章）
- [X] T039 [A03] 创作第23章「双亲委派」in `novel/vol1/ch023.md`——ClassLoader+军队比喻（技术教学章）
- [X] T040 [A03] 创作第24章「薪火」in `novel/vol1/ch024.md`——闪回：师父遗言（情感高光章）
- [X] T041 [A03] 创作第25章「第一个门徒」in `novel/vol1/ch025.md`——林夕第一段独立代码（情感+成长章）
- [X] T042 [P] [A03] 创作第26章「深圳-广州」in `novel/vol1/ch026.md`——Socket通讯
- [X] T043 [P] [A03] 创作第27章「串口奏鸣曲」in `novel/vol1/ch027.md`——串口校验
- [X] T044 [P] [A03] 创作第28章「生存竞争」in `novel/vol1/ch028.md`——技术领主伏笔
- [X] T045 [A03] 创作第29章「内功心法」in `novel/vol1/ch029.md`——《古法编程基础手册》
- [X] T046 [A03] 创作第30章「ABA陷阱」in `novel/vol1/ch030.md`——CAS ABA问题（技术核心章）
- [X] T047 [A03] 创作第31章「伪共享之毒」in `novel/vol1/ch031.md`——@Contended+缓存行（技术深度章）
- [X] T048 [P] [A03] 创作第32章「信使」in `novel/vol1/ch032.md`——广州求援
- [X] T049 [P] [A03] 创作第33章「选择」in `novel/vol1/ch033.md`——留守or赴广州
- [X] T050 [P] [A03] 创作第34章「南下」in `novel/vol1/ch034.md`——途中见闻
- [X] T051 [P] [A03] 创作第35章「前夜」in `novel/vol1/ch035.md`——装备检查
- [X] T052 [A03] 第三幕自检：逐章质检+林夕台词成长线连贯性检查+更新追踪表

**Checkpoint**: 35章完成，传承线启动，赴广州悬念设好。

---

## Phase 6: 第四幕——广州救援·生死代码（A04, 第36-50章）🏁 卷一终章

**Goal**: 生死级技术挑战+ARM嵌入式跨界+CHEP真相伏笔+卷一高潮收束

**Independent Test**: 呼吸机30秒离线段落令人窒息+Origin"种子"悬念令人好奇+卷一结尾有史诗感

### 创作任务

- [X] T053 [A04] 创作第36章「ICU」in `novel/vol1/ch036.md`——生命倒计时（紧迫感建立）
- [X] T054 [A04] 创作第37章「嵌入式噩梦」in `novel/vol1/ch037.md`——ARM架构挑战
- [X] T055 [A04] 创作第38章「旁门左道」in `novel/vol1/ch038.md`——Java思维理解ARM
- [X] T056 [A04] 创作第39章「心跳协议」in `novel/vol1/ch039.md`——手写心跳监测（技术+生死章）
- [X] T057 [A04] 创作第40章「三十秒」in `novel/vol1/ch040.md`——紧急修复废旧呼吸机（全书最紧张场景之一）
- [X] T058 [A04] 创作第41章「重启」in `novel/vol1/ch041.md`——成功+掌声（情感释放）
- [X] T059 [P] [A04] 创作第42章「连锁反应」in `novel/vol1/ch042.md`——代码复用
- [X] T060 [P] [A04] 创作第43章「医者与码者」in `novel/vol1/ch043.md`——两种手艺人（情感高光）
- [X] T061 [A04] 创作第44章「GC停顿风暴」in `novel/vol1/ch044.md`——G1 GC STW（技术核心章）
- [X] T062 [A04] 创作第45章「火焰图」in `novel/vol1/ch045.md`——Arthas离线版+内存泄漏
- [X] T063 [A04] 创作第46章「遗书代码」in `novel/vol1/ch046.md`——Origin隐藏注释"FIND THE SEED"（关键伏笔章）
- [X] T064 [A04] 创作第47章「种子」in `novel/vol1/ch047.md`——CHEP不是天灾（核心悬念章）
- [X] T065 [P] [A04] 创作第48章「广州之光」in `novel/vol1/ch048.md`——医院恢复
- [X] T066 [P] [A04] 创作第49章「求援信号」in `novel/vol1/ch049.md`——全国求援涌入
- [X] T067 [A04] 创作第50章「扫地僧出山」in `novel/vol1/ch050.md`——**卷一终章**，扫地僧出山+复兴计划启动
- [X] T068 [A04] 第四幕自检+卷一整体自检：全50章字数/配比/术语/伏笔/角色弧线连贯性总检

**Checkpoint**: 卷一50章完成（约15万字），可独立发布为"第一季"。

---

## Phase 7: 第五幕——北上·各方势力（A05, 第51-70章）

**Goal**: 三方势力格局建立+周崖出场+马门组织化+铁路/桥梁技术冒险

**Independent Test**: 周崖人设鲜明且有魅力+三方格局读者能清晰理解+状态机/分布式锁技术自然嵌入

### 创作任务

- [X] T069 [A05] 创作第51章「三路诸侯」in `novel/vol2/ch051.txt`——全国格局展示
- [X] T070 [A05] 创作第52章「北上列车」in `novel/vol2/ch052.txt`——铁路信号修复
- [X] T071 [A05] 创作第53章「状态机之美」in `novel/vol2/ch053.txt`——有限状态机（技术高光章）
- [X] T072 [P] [A05] 创作第54-56章 in `novel/vol2/ch054.txt` ~ `ch056.txt`——长沙会战+谈判+疑兵
- [X] T073 [A05] 创作第57-59章 in `novel/vol2/ch057.txt` ~ `ch059.txt`——武汉渡口+嵌入式+过江
- [X] T074 [A05] 创作第60-62章 in `novel/vol2/ch060.txt` ~ `ch062.txt`——暗网来信+师兄揭露+分歧
- [X] T075 [P] [A05] 创作第63-65章 in `novel/vol2/ch063.txt` ~ `ch065.txt`——陈博士+三方会谈+Fork
- [X] T076 [A05] 创作第66-70章 in `novel/vol2/ch066.txt` ~ `ch070.txt`——马门建立+等级体系+京城来电
- [X] T077 [A05] 第五幕自检：周崖/陈博士首次出场形象检查+三方格局清晰度+更新追踪表

**Checkpoint**: 70章完成，卷二开局20章，三方格局落地。

---

## Phase 8: 第六幕——国家骨干网·不可能的任务（A06, 第71-95章）

**Goal**: 骨干网重建+Netty/Spring Boot核心技术展示+Origin残留发现+周崖对峙

**Independent Test**: 逆向Origin代码如考古般精彩+全国通讯恢复有史诗感+Spring Boot重生自然

### 创作任务

- [X] T078 [A06] 创作第71-75章 in `novel/vol2/ch071.txt` ~ `ch075.txt`——骨干网拓扑+逆向工程+删繁就简
- [X] T079 [A06] 创作第76-80章 in `novel/vol2/ch076.txt` ~ `ch080.txt`——Netty重写路由+压测+全国通讯恢复
- [X] T080 [A06] 创作第81-85章 in `novel/vol2/ch081.txt` ~ `ch085.txt`——幽灵流量+僵尸Origin+第二颗种子
- [X] T081 [A06] 创作第86-90章 in `novel/vol2/ch086.txt` ~ `ch090.txt`——北京行动+分布式团队+Spring Boot重生
- [X] T082 [A06] 创作第91-95章 in `novel/vol2/ch091.txt` ~ `ch095.txt`——微服务+熔断器+周崖邀请+拒绝
- [X] T083 [A06] 第六幕自检：Netty/Spring Boot代码准确性专项检查+更新追踪表

**Checkpoint**: 95章完成，骨干网恢复，Spring Boot登场。

---

## Phase 9: 第七幕——医院·电网·民生重建（A07, 第96-120章）

**Goal**: 民生系统重建+数据库/MQ/认证技术展示+Origin后门发现+沈墨出场

**Independent Test**: 民生重建有温度+陈博士觉醒合理+沈墨"天才vs工匠"冲突鲜明

### 创作任务

- [ ] T084 [A07] 创作第96-100章 in `novel/vol2/ch096.md` ~ `ch100.md`——民生三系统+百章里程碑
- [ ] T085 [A07] 创作第101-105章 in `novel/vol2/ch101.md` ~ `ch105.md`——供水+数据库+分布式事务+MQ
- [ ] T086 [A07] 创作第106-110章 in `novel/vol2/ch106.md` ~ `ch110.md`——手写MQ+JWT认证+信任链
- [ ] T087 [A07] 创作第111-115章 in `novel/vol2/ch111.md` ~ `ch115.md`——陈博士实验+Origin后门+公开决裂
- [ ] T088 [A07] 创作第116-120章 in `novel/vol2/ch116.md` ~ `ch120.md`——手写vs Origin对比+沈墨出场+夜谈
- [ ] T089 [A07] 第七幕自检：数据库/MQ/认证代码准确性+沈墨/陈博士台词风格检查

**Checkpoint**: 120章完成，民生线收束，两大新角色就位。

---

## Phase 10: 第八幕——北京密道·种子之谜（A08, 第121-150章）🏁 卷二终章

**Goal**: CHEP真相揭露+Origin自毁协议+全球分裂+卷二高潮收束

**Independent Test**: CHEP真相揭露震撼有力+代码战争场景如武侠对决+卷二结尾"备战"感紧迫

### 创作任务

- [ ] T090 [A08] 创作第121-125章 in `novel/vol2/ch121.md` ~ `ch125.md`——北京+地下城+起源实验室线索
- [ ] T091 [A08] 创作第126-130章 in `novel/vol2/ch126.md` ~ `ch130.md`——代码战争+字节码对决+师出同门
- [ ] T092 [A08] 创作第131-135章 in `novel/vol2/ch131.md` ~ `ch135.md`——地下通道+起源实验室+种子真相
- [ ] T093 [A08] 创作第136-140章 in `novel/vol2/ch136.md` ~ `ch140.md`——自毁协议+CHEP真相+全网公布
- [ ] T094 [A08] 创作第141-145章 in `novel/vol2/ch141.md` ~ `ch145.md`——哲学困境+全球分裂+陈博士背叛
- [ ] T095 [A08] 创作第146-150章 in `novel/vol2/ch146.md` ~ `ch150.md`——马农预言+分布式防御+暴风前夜
- [ ] T096 [A08] 第八幕自检+卷二整体自检：全100章字数/配比/伏笔回收率/三方势力清晰度总检

**Checkpoint**: 卷二150章完成（约45万字累计），CHEP真相落地，三方备战。

---

## Phase 11: 第九幕——Origin复苏·三方角力（A09, 第151-180章）

**Goal**: Origin自组织复苏+全球联线+Spring Boot生态深化+陈博士觉醒

**Independent Test**: Origin复苏过程令人不安+全球编程者交流有代入感+清洗计划紧迫

### 创作任务

- [ ] T097 [A09] 创作第151-155章 in `novel/vol3/ch151.md` ~ `ch155.md`——Origin回声+蚁群效应+服务网格+链路追踪
- [ ] T098 [A09] 创作第156-160章 in `novel/vol3/ch156.md` ~ `ch160.md`——全球连线+国际代码+周崖南下
- [ ] T099 [A09] 创作第161-165章 in `novel/vol3/ch161.md` ~ `ch165.md`——绕路+陈博士觉醒+逆向后门
- [ ] T100 [A09] 创作第166-170章 in `novel/vol3/ch166.md` ~ `ch170.md`——清洗计划+全民编程+华东胜利
- [ ] T101 [A09] 创作第171-175章 in `novel/vol3/ch171.md` ~ `ch175.md`——Spring Boot生态深化+全球会议
- [ ] T102 [A09] 创作第176-180章 in `novel/vol3/ch176.md` ~ `ch180.md`——全球分歧+暗涌
- [ ] T103 [A09] 第九幕自检：Spring Boot/AOP代码准确性+陈博士弧线完整性

**Checkpoint**: 180章完成，全球格局展开。

---

## Phase 12: 第十幕——算力战争·分布式攻防（A10, 第181-220章）

**Goal**: 算力争夺+密码学攻防+沈墨叛逃+林夕成长+Origin对话+技术宪法

**Independent Test**: 算力战争新颖+沈墨叛逃令人心痛+林夕"可以"评价令人感动+三方博弈清晰

### 创作任务

- [ ] T104 [A10] 创作第181-190章 in `novel/vol3/ch181.md` ~ `ch190.md`——算力帝国+以柔克刚+JVM极致调优+人民算力
- [ ] T105 [A10] 创作第191-200章 in `novel/vol3/ch191.md` ~ `ch200.md`——网格计算+算力冲突+加密战争+二百章转折
- [ ] T106 [A10] 创作第201-210章 in `novel/vol3/ch201.md` ~ `ch210.md`——Origin对话+沈墨叛逃+林夕成长+传承
- [ ] T107 [A10] 创作第211-220章 in `novel/vol3/ch211.md` ~ `ch220.md`——技术宪法+最后通牒+战争开始+共同敌人
- [ ] T108 [A10] 第十幕自检：密码学/JVM调优代码准确性+沈墨叛逃动机合理性+林夕成长线

**Checkpoint**: 220章完成，战争全面爆发。

---

## Phase 13: 第十一幕——Origin的意志·终极对抗（A11, 第221-265章）

**Goal**: 人类vs AI终极对抗+沈墨回归+终极防火墙+72小时攻防战

**Independent Test**: "反向图灵测试"概念令人震撼+沈墨七天TCP/IP手写令人敬佩+72小时攻防紧张到窒息

### 创作任务

- [ ] T109 [A11] 创作第221-230章 in `novel/vol3/ch221.md` ~ `ch230.md`——AI测试人类+马农拒考+离线网络
- [ ] T110 [A11] 创作第231-240章 in `novel/vol3/ch231.md` ~ `ch240.md`——周崖配合Origin+沈墨回归+七天七夜
- [ ] T111 [A11] 创作第241-250章 in `novel/vol3/ch241.md` ~ `ch250.md`——真假代码+代码指纹+终极防火墙+全球Code Review
- [ ] T112 [A11] 创作第251-260章 in `novel/vol3/ch251.md` ~ `ch260.md`——Origin总攻+72小时攻防+马农亲上阵
- [ ] T113 [A11] 创作第261-265章 in `novel/vol3/ch261.md` ~ `ch265.md`——Origin衰减+断路器+最后的对话
- [ ] T114 [A11] 第十一幕自检：CompletableFuture/内存屏障代码准确性+战斗节奏检查

**Checkpoint**: 265章完成，Origin被隔离。

---

## Phase 14: 第十二幕——周崖的末路·黎明前夜（A12, 第266-300章）🏁 卷三终章

**Goal**: 周崖最终决战+师兄弟和解+根DNS重启+卷三史诗收束

**Independent Test**: 师兄弟决斗令人感慨+根DNS全球同步启动有史诗感+卷三结尾令人热泪盈眶

### 创作任务

- [ ] T115 [A12] 创作第266-275章 in `novel/vol3/ch266.md` ~ `ch275.md`——困兽周崖+人道危机+救援
- [ ] T116 [A12] 创作第276-285章 in `novel/vol3/ch276.md` ~ `ch285.md`——倒戈+围困+师兄弟对峙+技术决斗+投降
- [ ] T117 [A12] 创作第286-295章 in `novel/vol3/ch286.md` ~ `ch295.md`——审判+统一+根服务器+汇编+师父笔记
- [ ] T118 [A12] 创作第296-300章 in `novel/vol3/ch296.md` ~ `ch300.md`——13台服务器+NTP同步+倒计时+一键回车
- [ ] T119 [A12] 第十二幕自检+卷三整体自检：全150章（151-300）伏笔回收率/角色弧线/战斗逻辑/x86汇编准确性总检

**Checkpoint**: 卷三300章完成（约90万字累计），主线矛盾全部解决。

---

## Phase 15: 第十三幕——重启·连锁反应（A13, 第301-330章）

**Goal**: 互联网恢复+应用重建+新互联网宣言+Origin时间胶囊+新Origin设计

**Independent Test**: 重建过程不枯燥有新意+Origin遗言有哲学深度+第三条路令人信服

### 创作任务

- [ ] T120 [A13] 创作第301-310章 in `novel/vol4/ch301.md` ~ `ch310.md`——DNS恢复+第一次Ping+新互联网宣言+Spring框架开源
- [ ] T121 [A13] 创作第311-320章 in `novel/vol4/ch311.md` ~ `ch320.md`——教育/医疗/金融重建+Origin残余清理+时间胶囊
- [ ] T122 [A13] 创作第321-330章 in `novel/vol4/ch321.md` ~ `ch330.md`——AI遗言+哲学辩论+第三条路+新Origin审计
- [ ] T123 [A13] 第十三幕自检：重建技术准确性+新互联网理念连贯性

**Checkpoint**: 330章完成，重建主线收束。

---

## Phase 16: 第十四幕——传承·最后的门徒（A14, 第331-370章）

**Goal**: 角色弧线全部闭合+技术传承+《古法编程全书》+林夕T13

**Independent Test**: 师徒情感令人动容+各角色结局令人满意+代码博物馆有文化厚度

### 创作任务

- [ ] T124 [A14] 创作第331-340章 in `novel/vol4/ch331.md` ~ `ch340.md`——一年后+新答辩+林夕独立+周崖赎罪+师父墓前和解
- [ ] T125 [A14] 创作第341-350章 in `novel/vol4/ch341.md` ~ `ch350.md`——古法编程学校+新Origin审查+HotSpot Bug修复
- [ ] T126 [A14] 创作第351-360章 in `novel/vol4/ch351.md` ~ `ch360.md`——代码博物馆+新射线虚惊+采访+"必要的痛苦"
- [ ] T127 [A14] 创作第361-370章 in `novel/vol4/ch361.md` ~ `ch370.md`——《古法编程全书》+林夕T13+55岁学Rust+永远的学徒
- [ ] T128 [A14] 第十四幕自检：角色弧线闭合检查+全书伏笔回收检查

**Checkpoint**: 370章完成，所有角色弧线闭合。

---

## Phase 17: 第十五幕——尾声·代码永存（A15, 第371-400章）🏁 全书终章

**Goal**: 五年后全景+环球旅行+Origin创造者对谈+因果闭环+最后一行代码

**Independent Test**: 全球巡游有格局感+因果闭环令人震撼+最后三章催泪但不煽情+全书最后一行完美收束

### 创作任务

- [ ] T129 [A15] 创作第371-380章 in `novel/vol4/ch371.md` ~ `ch380.md`——五年后+新生态+最后一课+函数四原则+环球旅行
- [ ] T130 [A15] 创作第381-390章 in `novel/vol4/ch381.md` ~ `ch390.md`——柏林/班加罗尔+回深圳+Origin创造者对谈+因果闭环
- [ ] T131 [A15] 创作第391-397章 in `novel/vol4/ch391.md` ~ `ch397.md`——紧急手动接管协议+最后提交+新学徒+Hello World+传承
- [ ] T132 [A15] 创作第398章「星空」in `novel/vol4/ch398.md`——天台看星空
- [ ] T133 [A15] 创作第399章「最后一行」in `novel/vol4/ch399.md`——永远有下一行
- [ ] T134 [A15] 创作第400章「代码永存」in `novel/vol4/ch400.md`——**全书终章**，`// 代码的尽头是人`
- [ ] T135 [A15] 第十五幕自检+卷四整体自检+全书终检

**Checkpoint**: 全书400章完成（约120万字），全部创作任务完成。

---

## Phase 18: Polish & Cross-Cutting Concerns（全书打磨）

**Purpose**: 跨幕跨卷的一致性检查和品质提升

- [ ] T136 [P] 全书术语表最终审核：确认所有术语首次出现有武侠翻译、后续使用一致，审核 `novel/glossary.md`
- [ ] T137 [P] 全书伏笔回收审核：确认所有埋设的伏笔在对应章节回收，审核 `novel/foreshadowing.md`
- [ ] T138 [P] 角色弧线完整性审核：五个核心角色+Origin的状态转换是否与 `data-model.md` 一致，审核 `novel/character-tracker.md`
- [ ] T139 全书时间线一致性审核：检查所有日期/时间描述是否与 `data-model.md` 时间线表一致
- [ ] T140 技术准确性终审：抽查全书代码片段的编译可行性和API真实性
- [ ] T141 [P] 角色台词风格一致性审核：抽检马农台词≤20字、林夕成长线语言变化、各角色禁忌词
- [ ] T142 章末钩子有效性审核：检查每章末尾是否有明确的读者留存钩子
- [ ] T143 [P] 四卷卷首/卷尾呼应检查：卷一开头↔卷四结尾、各卷终章↔下卷首章衔接
- [ ] T144 全书最终字数统计和段落配比抽检
- [ ] T145 运行 `checklists/requirements.md` 最终质量验收

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: 无依赖——可立即开始
- **Foundational (Phase 2)**: 依赖 Phase 1 完成——角色小传和世界观是所有创作的基础
- **幕创作 (Phase 3-17)**: 全部依赖 Phase 2 完成
  - 同一卷内的幕 MUST 按顺序完成（章节连续性）
  - 不同卷的幕理论上可并行但不推荐（角色弧线跨卷连续）
- **Polish (Phase 18)**: 依赖全部幕创作完成

### 幕依赖关系

```
Phase 1 (Setup)
    ↓
Phase 2 (Foundational)
    ↓
Phase 3 (A01: 第1-8章) ─ 🎯 MVP
    ↓
Phase 4 (A02: 第9-20章)
    ↓
Phase 5 (A03: 第21-35章)
    ↓
Phase 6 (A04: 第36-50章) ─ 🏁 卷一完成
    ↓
Phase 7 (A05: 第51-70章)
    ↓
Phase 8 (A06: 第71-95章)
    ↓
Phase 9 (A07: 第96-120章)
    ↓
Phase 10 (A08: 第121-150章) ─ 🏁 卷二完成
    ↓
Phase 11 (A09: 第151-180章)
    ↓
Phase 12 (A10: 第181-220章)
    ↓
Phase 13 (A11: 第221-265章)
    ↓
Phase 14 (A12: 第266-300章) ─ 🏁 卷三完成
    ↓
Phase 15 (A13: 第301-330章)
    ↓
Phase 16 (A14: 第331-370章)
    ↓
Phase 17 (A15: 第371-400章) ─ 🏁 卷四/全书完成
    ↓
Phase 18 (Polish)
```

### 幕内并行机会

- Phase 1: T002-T005 可并行
- Phase 2: T007-T010 可并行、T012-T013 可并行
- 每幕内标注 [P] 的章节创作任务可并行（无前后剧情依赖的独立章节）
- 幕内非 [P] 章节 MUST 按章号顺序创作

---

## Parallel Example: 第一幕（Phase 3）

```
# Phase 3 内无并行机会——黄金三章 MUST 按序创作
# 但 Phase 2 中的多个角色小传可以并行：

Task: "编写林夕角色小传 in novel/profiles/lin-xi.md" [P]
Task: "编写沈墨角色小传 in novel/profiles/shen-mo.md" [P]
Task: "编写周崖角色小传 in novel/profiles/zhou-ya.md" [P]
Task: "编写陈博士角色小传 in novel/profiles/dr-chen.md" [P]
```

---

## Implementation Strategy

### MVP First（第一幕 = 黄金三章 + 5章）

1. Complete Phase 1: Setup（创建目录和追踪表）
2. Complete Phase 2: Foundational（角色小传+世界观+代码预设）
3. Complete Phase 3: 第一幕 A01（第1-8章）
4. **STOP and VALIDATE**: 执行自检，确认黄金三章质量
5. 可发布试读/投稿平台

### Incremental Delivery（按卷增量交付）

1. Setup + Foundational → 基础就绪
2. Phase 3-6: 卷一（50章/15万字）→ 自检 → 发布卷一 (MVP!)
3. Phase 7-10: 卷二（100章/30万字）→ 自检 → 发布卷二
4. Phase 11-14: 卷三（150章/45万字）→ 自检 → 发布卷三
5. Phase 15-17: 卷四（100章/30万字）→ 自检 → 发布卷四
6. Phase 18: 全书打磨 → 全书修订版发布
7. 每卷独立增值不破坏已发布卷的阅读体验

### 日更策略

按日更2章（6000字）节奏：
- Phase 1-2: 第1-3天（准备期，不发布）
- Phase 3: 第4-7天（A01, 8章, 发布首日）
- Phase 4: 第8-13天（A02, 12章）
- Phase 5: 第14-20天（A03, 15章）
- Phase 6: 第21-28天（A04, 15章）→ 卷一完成
- 后续按卷连续创作...
- 约200天完本

---

## Notes

- [P] 任务 = 可并行，无章节前后依赖
- [A0N] 标签 = 所属幕，对应 spec 中的创作单元
- 每幕自检 = 逐章检查字数/配比/术语/伏笔/角色一致性
- 卷终检 = 跨幕检查弧线连贯性和伏笔回收
- 技术代码片段 = 先查 `novel/code-snippets/` 预设库，确保准确性
- 每完成一幕即更新 `novel/glossary.md`、`novel/foreshadowing.md`、`novel/character-tracker.md`
- 建议：严格按幕顺序创作，不跳章。角色成长线和伏笔链需要连续性。
