# Implementation Plan: 《全球AI编程失效，只有我会古法编程》400章创作

**Branch**: `main` | **Date**: 2026-03-09 | **Spec**: [spec.md](./spec.md)
**Input**: 400章编写思路规格，含四卷独立文件（vol1-vol4.md）

## Summary

创作一部400章、约120万字的网络技术流小说。故事设定在2038年，超级AI"Origin"覆盖99%代码生产后突然崩溃，主角马农（38岁，前腾讯T13）凭借古法编程从废墟中重建文明。全书分四卷十五幕，以"技术爽感如武侠"为核心卖点，采用偏大众向的写作定位（技术10%+叙事50%+情感40%），代码量≤2%，重点在剧情+叙事+情感。

## Technical Context

**类型/体裁**: 网络文学·技术流·末日重建  
**目标平台**: 起点中文网/番茄小说等网文平台  
**体量规格**: 400章 × 3000字/章 ≈ 120万字  
**写作配比**: 技术描写10%（~300字/章）+ 叙事推进50%（~1500字/章）+ 情感/对话40%（~1200字/章）；代码量≤2%（~60字/章），技术爽感通过叙事+武侠比喻传递  
**技术栈（小说内）**: Java（JDK 17 LTS为主线）+ ARM嵌入式C/汇编（辅线）+ Spring Boot/Netty（中后期）  
**更新节奏**: 待定（建议日更2章=6000字，约200天完本）  
**叙事结构**: 四卷十五幕，黄金三章节奏（重生反击→预言成真→技术封神）  
**目标读者**: 程序员+泛科技爱好者+末日文读者

## Constitution Check

*GATE: 宪章合规性检查——创作前必须通过*

| 原则 | 状态 | 验证 |
|------|------|------|
| I. 技术武侠化 | ✅ PASS | 大纲中所有技术场景均有武侠映射（走火入魔/号脉/千军万马等） |
| II. 古法编程至上 | ✅ PASS | 马农始终手写代码，技能树完整（内存微操/架构直觉/古法工具箱/Java底层） |
| III. 黄金三章节奏 | ✅ PASS | 四卷节奏差异化设计，每卷有明确的三拍循环周期 |
| IV. Java技术栈准确 | ✅ PASS | JDK 17 LTS为主线，涉及JVM/并发/Spring Boot/Netty均为真实技术 |
| V. 硬核不晦涩 | ✅ PASS | 三层叙事结构+技术10%占比+代码≤2%，偏大众向，重点在剧情/叙事/情感，技术爽感靠叙事传递 |
| 世界观约束 | ⚠️ 需修正 | 宪章中时间线仍写"2028年"，需同步修正为"2038年"（已在clarify中确认） |
| 角色规范 | ✅ PASS | 马农性格五MUST/三MUST NOT完整，叙事语言风格明确 |

**Gate 结果**: PASS（世界观时间线需同步修正，不阻塞规划）

## Project Structure

### 创作文件架构

```text
specs/1-novel-chapter-outline/
├── spec.md              # 总览索引+澄清记录
├── plan.md              # 本文件：创作实施计划
├── research.md          # Phase 0：创作研究与决策
├── data-model.md        # Phase 1：角色/世界观数据模型
├── contracts/           # Phase 1：写作规范契约
│   ├── chapter-format.md    # 单章格式规范
│   ├── tech-writing.md      # 技术描写规范
│   └── character-voice.md   # 角色语言风格规范
├── quickstart.md        # Phase 1：快速启动指南（首章写作指引）
├── vol1.md              # 卷一章节大纲
├── vol2.md              # 卷二章节大纲
├── vol3.md              # 卷三章节大纲
├── vol4.md              # 卷四章节大纲
└── checklists/
    └── requirements.md  # 质量检查清单
```

### 小说文件架构（待创建）

```text
novel/
├── vol1/               # 卷一：危机爆发与降维打击
│   ├── ch001.md ~ ch050.md
├── vol2/               # 卷二：废墟技术领主
│   ├── ch051.md ~ ch150.md
├── vol3/               # 卷三：全球算力争夺战
│   ├── ch151.md ~ ch300.md
└── vol4/               # 卷四：代码重燃文明重启
    ├── ch301.md ~ ch400.md
```

**Structure Decision**: 按卷分目录，每章独立md文件，便于版本管理和并行创作。

## Complexity Tracking

> 无宪章违规需要论证。

## Constitution Re-Check (Post Phase 1)

*Phase 1 设计完成后的二次宪章合规检查*

| 原则 | 状态 | 验证 |
|------|------|------|
| I. 技术武侠化 | ✅ PASS | tech-writing.md 定义了18组技术→武侠映射表，覆盖全书核心技术场景 |
| II. 古法编程至上 | ✅ PASS | data-model.md 明确马农技能树和"扫地僧"行为模式 |
| III. 黄金三章节奏 | ✅ PASS | chapter-format.md 要求每章标注"情感节拍"位置 |
| IV. Java技术栈准确 | ✅ PASS | tech-writing.md 要求代码可编译、API真实、JDK 17 LTS |
| V. 硬核不晦涩 | ✅ PASS | 三层叙事结构已编入tech-writing.md，术语首次武侠翻译规则已定义 |
| 世界观约束 | ✅ PASS | 宪章时间线已修正为2038年，data-model.md时间线完整 |
| 角色规范 | ✅ PASS | character-voice.md 为5个核心角色定义了语言风格+示例库 |

**Gate 结果**: ✅ ALL PASS — 可以进入 `/speckit.tasks` 阶段。
