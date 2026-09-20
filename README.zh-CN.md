# Mystilink 库索引

> Languages: [English](README.md) | [简体中文](README.zh-CN.md)

## 概述

Mystilink 计算类库、数据结构契约、本地 MCP 集成与 Agent Skill 包索引。每个项目均为本根目录下的独立仓库。安装与运行方式见各项目 README。

## 计算器

| 目录 | CLI | 能力 |
|------|-----|------|
| `mystilink-lunar-calendar` | `lunar` | 公农互转、闰月、年柱/生肖、JSON |
| `mystilink-bazi-calculator` | `bazi` | 四柱、大运、流年 |
| `mystilink-ziwei-calculator` | `ziwei` | 紫微斗数命盘 |
| `mystilink-horoscope-calculator` | `horoscope` | 本命盘、日运（行运）、月运 |
| `mystilink-tarot-calculator` | `tarot` | 韦特塔罗抽牌（牌阵、正逆位） |
| `mystilink-liuyao-calculator` | `liuyao` | 六爻铜钱起卦（本卦/之卦） |

计算器仓库遵循语言矩阵：C、C++、C#、Java、JavaScript（Node + Browser 注入）、Python。

主 CLI 为短命令（`bazi`、`ziwei`、`horoscope`、`lunar`、`tarot`、`liuyao`）。长别名（`mystilink-*`）仍会安装以保持兼容。
可选 `--envelope` 将盘面包装为 `mystilink.envelope/0.1`。

## 数据结构契约

| 目录 | 作用 |
|------|------|
| `mystilink-metaphysics-schema` | 出生档案、历法基座、信封与体系盘面的共用 JSON Schema |

契约仓为文档/schema 包，**不适用**计算器语言矩阵（见项目 README）。

## 本地 MCP

| 目录 | CLI | 能力 |
|------|-----|------|
| `mystilink-mcp` | `mystilink-mcp` | 基于计算器 CLI 的 stdio MCP tools；可选本机 `127.0.0.1` FastAPI |

MCP / 本地集成包。**不适用**计算器语言矩阵。**不提供**对外 http/https 远程服务。

```bash
cd mystilink-mcp && python3 -m pip install -e .
mystilink-mcp status
mystilink-mcp stdio
```

## Agent Skills

| 目录 | Skill `name` | 能力 |
|------|--------------|------|
| `mystilink-router-skill` | `mystilink-router` | 选择单一体系 skill |
| `mystilink-bazi-skill` | `mystilink-bazi` | 八字排盘脚本 + 解读工作流 |
| `mystilink-ziwei-skill` | `mystilink-ziwei` | 紫微排盘脚本 + 解读工作流 |
| `mystilink-horoscope-skill` | `mystilink-horoscope` | 本命盘脚本 + 解读工作流 |
| `mystilink-tarot-skill` | `mystilink-tarot` | 抽牌脚本 + 解读工作流 |
| `mystilink-liuyao-skill` | `mystilink-liuyao` | 起卦脚本 + 解读工作流 |

Skill 仓库为 Agent Skill 包（`SKILL.md` + 可选 `scripts/`）。**不适用**计算器语言矩阵。安装时复制到宿主 skills 目录，目录名使用 skill 的 `name`。

## 快速开始（计算器）

```bash
cd mystilink-lunar-calendar && python3 -m pip install -e .
lunar convert --date 1993-09-28 --time 13:21 --timezone Asia/Shanghai --json

cd ../mystilink-bazi-calculator && python3 -m pip install -e .
bazi calculate --date 1990-05-15 --hour 12

cd ../mystilink-ziwei-calculator && python3 -m pip install -e .
ziwei chart --datetime "1990-05-15 14:30" --timezone Asia/Shanghai --gender male

cd ../mystilink-horoscope-calculator && python3 -m pip install -e .
horoscope natal --datetime "1990-05-15 14:30" --timezone Asia/Shanghai --lat 31.2 --lon 121.5

cd ../mystilink-tarot-calculator && python3 -m pip install -e .
tarot draw --seed 123

cd ../mystilink-liuyao-calculator && python3 -m pip install -e .
liuyao cast --seed 123
```

## 快速开始（Skills）

```bash
cp -R mystilink-bazi-skill /path/to/.cursor/skills/mystilink-bazi
python3 /path/to/.cursor/skills/mystilink-bazi/scripts/bazi_calculate.py --date 1990-05-15 --hour 12
```

## 共同约定

- MIT License
- 多语言 README，文首语言互链
- 计算器：语言矩阵 C / C++ / C# / Java / JavaScript（Node + Browser）/ Python
- 计算器 CLI：短命令 `bazi` / `ziwei` / `horoscope` / `lunar` / `tarot` / `liuyao`（长别名 `mystilink-*` 保留）
- 可选 `--envelope`（`mystilink.envelope/0.1`）
- 数据结构契约：JSON Schema + 示例；不适用语言矩阵
- `mystilink-mcp`：本地 stdio MCP（+ 可选 `127.0.0.1` FastAPI）；不适用语言矩阵
- Skills：Agent Skill 布局；不适用语言矩阵（各 skill README 已声明）
- 计算器核心计算不依赖仓库内远程资源 URL
- Cursor Rules 位于各仓库与本索引仓库的 `.cursor/rules/`（仅本地，不发布）
