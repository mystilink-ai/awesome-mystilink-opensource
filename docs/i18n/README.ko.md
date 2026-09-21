# Mystilink 라이브러리 색인

> Languages: [English](../../README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Français](README.fr.md) | [Español](README.es.md)

## 개요

Mystilink 계산 라이브러리, 스키마 계약, 로컬 MCP 통합, Agent Skill 패키지 색인입니다. 각 프로젝트는 이 루트 아래의 독립 저장소입니다. 설치와 실행 방법은 각 프로젝트 README를 참고하세요.

## 계산기

| 디렉터리 | CLI | 기능 |
|-----------|-----|------|
| `mystilink-lunar-calendar` | `lunar` | 그레고리력↔음력, 윤달, 연간지/띠, JSON |
| `mystilink-bazi-calculator` | `bazi` | 사주, 대운, 유년 |
| `mystilink-ziwei-calculator` | `ziwei` | 자미두수 명반 |
| `mystilink-horoscope-calculator` | `horoscope` | 네이탈, 일운(트랜싯), 월운 |
| `mystilink-tarot-calculator` | `tarot` | RWS 드로우(스프레드, 정/역위치) |
| `mystilink-liuyao-calculator` | `liuyao` | 육효 동전 기괘(본괘/지괘) |

계산기 저장소는 언어 매트릭스를 따릅니다: C, C++, C#, Java, JavaScript(Node + Browser 주입), Python.

주 CLI는 짧은 이름(`bazi`, `ziwei`, `horoscope`, `lunar`, `tarot`, `liuyao`)입니다. 긴 별칭(`mystilink-*`)은 호환을 위해 계속 설치됩니다.
선택적 `--envelope`는 차트 JSON을 `mystilink.envelope/0.1`로 감쌉니다.

## 스키마 계약

| 디렉터리 | 역할 |
|-----------|------|
| `mystilink-metaphysics-schema` | 출생 프로필, 역법 기반, 엔벨로프, 체계 차트의 공유 JSON Schema |

스키마 저장소는 문서/계약 패키지입니다. 계산기 언어 매트릭스는 **적용하지 않습니다**(프로젝트 README에 명시).

## 로컬 MCP

| 디렉터리 | CLI | 기능 |
|-----------|-----|------|
| `mystilink-mcp` | `mystilink-mcp` | 계산기 CLI 위 stdio MCP tools; 선택적 `127.0.0.1` 루프백 FastAPI |

MCP / 로컬 통합 패키지입니다. 계산기 언어 매트릭스는 **적용하지 않습니다**. 원격 HTTP/HTTPS 서비스는 **제공하지 않습니다**.

```bash
cd mystilink-mcp && python3 -m pip install -e .
mystilink-mcp status
mystilink-mcp stdio
```

## Agent Skills

| 디렉터리 | Skill `name` | 기능 |
|-----------|--------------|------|
| `mystilink-router-skill` | `mystilink-router` | 단일 체계 skill 선택 |
| `mystilink-bazi-skill` | `mystilink-bazi` | 팔자 배반 스크립트 + 해석 워크플로 |
| `mystilink-ziwei-skill` | `mystilink-ziwei` | 자미 배반 스크립트 + 해석 워크플로 |
| `mystilink-horoscope-skill` | `mystilink-horoscope` | 네이탈 차트 스크립트 + 해석 워크플로 |
| `mystilink-tarot-skill` | `mystilink-tarot` | 드로우 스크립트 + 해석 워크플로 |
| `mystilink-liuyao-skill` | `mystilink-liuyao` | 기괘 스크립트 + 해석 워크플로 |

Skill 저장소는 Agent Skill 패키지(`SKILL.md` + 선택 `scripts/`)입니다. 계산기 언어 매트릭스는 **적용하지 않습니다**. 호스트 skills 디렉터리에 skill `name`을 폴더명으로 복사해 설치합니다.

## 빠른 시작(계산기)

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

## 빠른 시작(Skills)

```bash
cp -R mystilink-bazi-skill /path/to/.cursor/skills/mystilink-bazi
python3 /path/to/.cursor/skills/mystilink-bazi/scripts/bazi_calculate.py --date 1990-05-15 --hour 12
```

## 공통 규약

- MIT License
- 다국어 README(상단 언어 전환 링크)
- 계산기: 언어 매트릭스 C / C++ / C# / Java / JavaScript(Node + Browser) / Python
- 계산기 CLI: 짧은 이름 `bazi` / `ziwei` / `horoscope` / `lunar` / `tarot` / `liuyao`(긴 `mystilink-*` 별칭 유지)
- 선택적 `--envelope`(`mystilink.envelope/0.1`)
- 스키마 계약: JSON Schema + 예제; 언어 매트릭스 비적용
- `mystilink-mcp`: 로컬 stdio MCP(+ 선택 `127.0.0.1` FastAPI); 언어 매트릭스 비적용
- Skills: Agent Skill 레이아웃; 언어 매트릭스 비적용(각 skill README에 명시)
- 계산기 핵심 연산에 원격 리소스 URL 불필요
- Cursor Rules는 각 저장소와 본 색인 저장소의 `.cursor/rules/`에 위치(로컬 전용, 게시하지 않음)
