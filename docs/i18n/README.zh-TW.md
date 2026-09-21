# Mystilink 函式庫索引

> Languages: [English](../../README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Français](README.fr.md) | [Español](README.es.md)

## 概述

Mystilink 計算類函式庫、資料結構契約、本地 MCP 整合與 Agent Skill 套件索引。每個專案均為本根目錄下的獨立倉庫。安裝與執行方式見各專案 README。

## 計算器

| 目錄 | CLI | 能力 |
|------|-----|------|
| `mystilink-lunar-calendar` | `lunar` | 公農互轉、閏月、年柱/生肖、JSON |
| `mystilink-bazi-calculator` | `bazi` | 四柱、大運、流年 |
| `mystilink-ziwei-calculator` | `ziwei` | 紫微斗數命盤 |
| `mystilink-horoscope-calculator` | `horoscope` | 本命盤、日運（行運）、月運 |
| `mystilink-tarot-calculator` | `tarot` | 偉特塔羅抽牌（牌陣、正逆位） |
| `mystilink-liuyao-calculator` | `liuyao` | 六爻銅錢起卦（本卦/之卦） |

計算器倉庫遵循語言矩陣：C、C++、C#、Java、JavaScript（Node + Browser 注入）、Python。

主 CLI 為短命令（`bazi`、`ziwei`、`horoscope`、`lunar`、`tarot`、`liuyao`）。長別名（`mystilink-*`）仍會安裝以保持相容。
可選 `--envelope` 將盤面包裝為 `mystilink.envelope/0.1`。

## 資料結構契約

| 目錄 | 作用 |
|------|------|
| `mystilink-metaphysics-schema` | 出生檔案、曆法基座、信封與體系盤面的共用 JSON Schema |

契約倉為文件/schema 套件，**不適用**計算器語言矩陣（見專案 README）。

## 本地 MCP

| 目錄 | CLI | 能力 |
|------|-----|------|
| `mystilink-mcp` | `mystilink-mcp` | 基於計算器 CLI 的 stdio MCP tools；可選本機 `127.0.0.1` FastAPI |

MCP / 本地整合套件。**不適用**計算器語言矩陣。**不提供**對外 http/https 遠端服務。

```bash
cd mystilink-mcp && python3 -m pip install -e .
mystilink-mcp status
mystilink-mcp stdio
```

## Agent Skills

| 目錄 | Skill `name` | 能力 |
|------|--------------|------|
| `mystilink-router-skill` | `mystilink-router` | 選擇單一體系 skill |
| `mystilink-bazi-skill` | `mystilink-bazi` | 八字排盤腳本 + 解讀工作流 |
| `mystilink-ziwei-skill` | `mystilink-ziwei` | 紫微排盤腳本 + 解讀工作流 |
| `mystilink-horoscope-skill` | `mystilink-horoscope` | 本命盤腳本 + 解讀工作流 |
| `mystilink-tarot-skill` | `mystilink-tarot` | 抽牌腳本 + 解讀工作流 |
| `mystilink-liuyao-skill` | `mystilink-liuyao` | 起卦腳本 + 解讀工作流 |

Skill 倉庫為 Agent Skill 套件（`SKILL.md` + 可選 `scripts/`）。**不適用**計算器語言矩陣。安裝時複製到宿主 skills 目錄，目錄名使用 skill 的 `name`。

## 快速開始（計算器）

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

## 快速開始（Skills）

```bash
cp -R mystilink-bazi-skill /path/to/.cursor/skills/mystilink-bazi
python3 /path/to/.cursor/skills/mystilink-bazi/scripts/bazi_calculate.py --date 1990-05-15 --hour 12
```

## 共同約定

- MIT License
- 多語言 README，文首語言互鏈
- 計算器：語言矩陣 C / C++ / C# / Java / JavaScript（Node + Browser）/ Python
- 計算器 CLI：短命令 `bazi` / `ziwei` / `horoscope` / `lunar` / `tarot` / `liuyao`（長別名 `mystilink-*` 保留）
- 可選 `--envelope`（`mystilink.envelope/0.1`）
- 資料結構契約：JSON Schema + 範例；不適用語言矩陣
- `mystilink-mcp`：本地 stdio MCP（+ 可選 `127.0.0.1` FastAPI）；不適用語言矩陣
- Skills：Agent Skill 佈局；不適用語言矩陣（各 skill README 已聲明）
- 計算器核心計算不依賴倉庫內遠端資源 URL
- Cursor Rules 位於各倉庫與本索引倉庫的 `.cursor/rules/`（僅本地，不發布）
