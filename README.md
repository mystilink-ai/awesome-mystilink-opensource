# Mystilink Libraries Index

> Languages: [English](README.md) | [简体中文](README.zh-CN.md)

## Overview

Index of Mystilink calculation libraries, schema contracts, and Agent Skill packages. Each project is an independent repository under this root. Install and run locally with the commands in each project README.

## Calculators

| Directory | CLI | Capabilities |
|-----------|-----|--------------|
| `mystilink-lunar-calendar` | `lunar` | Gregorian↔lunar, leap months, year ganzhi/zodiac, JSON |
| `mystilink-bazi-calculator` | `bazi` | Four Pillars, DaYun, LiuNian |
| `mystilink-ziwei-calculator` | `ziwei` | Zi Wei Dou Shu chart |
| `mystilink-horoscope-calculator` | `horoscope` | Natal, daily transit, monthly transit |
| `mystilink-tarot-calculator` | `tarot` | RWS draw (spreads, upright/reversed) |
| `mystilink-liuyao-calculator` | `liuyao` | Six-line coin cast (ben/zhi) |

Calculator repos follow the language matrix: C, C++, C#, Java, JavaScript (Node + Browser inject), Python.

Primary CLI names are short (`bazi`, `ziwei`, `horoscope`, `lunar`, `tarot`, `liuyao`). Long aliases (`mystilink-*`) remain installed for compatibility.
Optional `--envelope` wraps chart JSON as `mystilink.envelope/0.1`.

## Schema contracts

| Directory | Role |
|-----------|------|
| `mystilink-metaphysics-schema` | Shared JSON Schema for birth profiles, calendar basis, envelopes, and system charts |

Schema repos are documentation/contract packages. They do **not** apply the calculator language matrix (stated in the project README).

## Agent Skills

| Directory | Skill `name` | Capabilities |
|-----------|--------------|--------------|
| `mystilink-router-skill` | `mystilink-router` | Choose one theory skill |
| `mystilink-bazi-skill` | `mystilink-bazi` | BaZi chart scripts + reading workflow |
| `mystilink-ziwei-skill` | `mystilink-ziwei` | Zi Wei chart script + reading workflow |
| `mystilink-horoscope-skill` | `mystilink-horoscope` | Natal chart script + reading workflow |
| `mystilink-tarot-skill` | `mystilink-tarot` | Draw script + reading workflow |
| `mystilink-liuyao-skill` | `mystilink-liuyao` | Cast script + reading workflow |

Skill repos are Agent Skill packages (`SKILL.md` + optional `scripts/`). They do **not** apply the calculator language matrix. Install by copying into the host skills directory using the skill `name` as the folder name.

## Quick start (calculators)

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

## Quick start (skills)

```bash
cp -R mystilink-bazi-skill /path/to/.cursor/skills/mystilink-bazi
python3 /path/to/.cursor/skills/mystilink-bazi/scripts/bazi_calculate.py --date 1990-05-15 --hour 12
```

## Shared conventions

- MIT License
- Multi-language README with header language switcher
- Calculators: language matrix C / C++ / C# / Java / JavaScript (Node + Browser) / Python
- Calculator CLIs: short names `bazi` / `ziwei` / `horoscope` / `lunar` / `tarot` / `liuyao` (long `mystilink-*` aliases kept)
- Optional `--envelope` on calculator CLIs for `mystilink.envelope/0.1`
- Schema contracts: JSON Schema + examples; language matrix not applicable
- Skills: Agent Skill layout; language matrix not applicable (stated in each skill README)
- No remote resource URLs required inside calculator trees for core compute
- Cursor rules live under each repo `.cursor/rules/` and this index repo (local only; not published)
