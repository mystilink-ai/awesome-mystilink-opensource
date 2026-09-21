# Mystilink ライブラリ索引

> Languages: [English](../../README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Français](README.fr.md) | [Español](README.es.md)

## 概要

Mystilink の計算ライブラリ、スキーマ契約、ローカル MCP 統合、Agent Skill パッケージの索引です。各プロジェクトはこのルート配下の独立リポジトリです。インストールと実行方法は各プロジェクトの README を参照してください。

## 計算機

| ディレクトリ | CLI | 機能 |
|-----------|-----|------|
| `mystilink-lunar-calendar` | `lunar` | グレゴリオ暦↔旧暦、閏月、年干支/十二支、JSON |
| `mystilink-bazi-calculator` | `bazi` | 四柱、大運、流年 |
| `mystilink-ziwei-calculator` | `ziwei` | 紫微斗数命盤 |
| `mystilink-horoscope-calculator` | `horoscope` | ネイタル、日運（トランジット）、月運 |
| `mystilink-tarot-calculator` | `tarot` | RWS 抽牌（スプレッド、正位置/逆位置） |
| `mystilink-liuyao-calculator` | `liuyao` | 六爻銅銭起卦（本卦/之卦） |

計算機リポジトリは言語マトリクスに従います：C、C++、C#、Java、JavaScript（Node + Browser 注入）、Python。

主 CLI は短い名前（`bazi`、`ziwei`、`horoscope`、`lunar`、`tarot`、`liuyao`）です。長い別名（`mystilink-*`）は互換性のため引き続きインストールされます。
オプションの `--envelope` は盤面 JSON を `mystilink.envelope/0.1` で包みます。

## スキーマ契約

| ディレクトリ | 役割 |
|-----------|------|
| `mystilink-metaphysics-schema` | 出生プロフィール、暦基盤、エンベロープ、体系盤面の共有 JSON Schema |

スキーマリポジトリはドキュメント/契約パッケージです。計算機の言語マトリクスは**適用しません**（プロジェクト README に記載）。

## ローカル MCP

| ディレクトリ | CLI | 機能 |
|-----------|-----|------|
| `mystilink-mcp` | `mystilink-mcp` | 計算機 CLI 上の stdio MCP tools；オプションで `127.0.0.1` のループバック FastAPI |

MCP / ローカル統合パッケージです。計算機の言語マトリクスは**適用しません**。リモート HTTP/HTTPS サービスは**提供しません**。

```bash
cd mystilink-mcp && python3 -m pip install -e .
mystilink-mcp status
mystilink-mcp stdio
```

## Agent Skills

| ディレクトリ | Skill `name` | 機能 |
|-----------|--------------|------|
| `mystilink-router-skill` | `mystilink-router` | 単一体系 skill を選択 |
| `mystilink-bazi-skill` | `mystilink-bazi` | 八字排盤スクリプト + 解読ワークフロー |
| `mystilink-ziwei-skill` | `mystilink-ziwei` | 紫微排盤スクリプト + 解読ワークフロー |
| `mystilink-horoscope-skill` | `mystilink-horoscope` | ネイタル盤スクリプト + 解読ワークフロー |
| `mystilink-tarot-skill` | `mystilink-tarot` | 抽牌スクリプト + 解読ワークフロー |
| `mystilink-liuyao-skill` | `mystilink-liuyao` | 起卦スクリプト + 解読ワークフロー |

Skill リポジトリは Agent Skill パッケージ（`SKILL.md` + 任意の `scripts/`）です。計算機の言語マトリクスは**適用しません**。ホストの skills ディレクトリへ、skill の `name` をフォルダ名としてコピーしてインストールします。

## クイックスタート（計算機）

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

## クイックスタート（Skills）

```bash
cp -R mystilink-bazi-skill /path/to/.cursor/skills/mystilink-bazi
python3 /path/to/.cursor/skills/mystilink-bazi/scripts/bazi_calculate.py --date 1990-05-15 --hour 12
```

## 共通規約

- MIT License
- 多言語 README（先頭に言語切替リンク）
- 計算機：言語マトリクス C / C++ / C# / Java / JavaScript（Node + Browser）/ Python
- 計算機 CLI：短い名前 `bazi` / `ziwei` / `horoscope` / `lunar` / `tarot` / `liuyao`（長い `mystilink-*` 別名は維持）
- オプション `--envelope`（`mystilink.envelope/0.1`）
- スキーマ契約：JSON Schema + 例；言語マトリクス非適用
- `mystilink-mcp`：ローカル stdio MCP（+ 任意の `127.0.0.1` FastAPI）；言語マトリクス非適用
- Skills：Agent Skill レイアウト；言語マトリクス非適用（各 skill README に記載）
- 計算機のコア計算にリモートリソース URL は不要
- Cursor Rules は各リポジトリと本索引の `.cursor/rules/` に配置（ローカルのみ、公開しない）
