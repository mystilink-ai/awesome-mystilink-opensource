# Índice de bibliotecas Mystilink

> Languages: [English](../../README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Français](README.fr.md) | [Español](README.es.md)

## Resumen

Índice de bibliotecas de cálculo Mystilink, contratos de esquema, integración MCP local y paquetes Agent Skill. Cada proyecto es un repositorio independiente bajo esta raíz. Instalación y uso: consulte el README de cada proyecto.

## Calculadoras

| Directorio | CLI | Capacidades |
|-----------|-----|--------------|
| `mystilink-lunar-calendar` | `lunar` | Gregoriano↔lunar, meses intercalares, ganzhi/zodiaco anual, JSON |
| `mystilink-bazi-calculator` | `bazi` | Cuatro Pilares (BaZi), DaYun, LiuNian |
| `mystilink-ziwei-calculator` | `ziwei` | Carta Zi Wei Dou Shu |
| `mystilink-horoscope-calculator` | `horoscope` | Natal, tránsito diario, tránsito mensual |
| `mystilink-tarot-calculator` | `tarot` | Tirada RWS (tiradas, derecha/invertida) |
| `mystilink-liuyao-calculator` | `liuyao` | Tirada de seis líneas (ben/zhi) |

Los repositorios de calculadoras siguen la matriz de lenguajes: C, C++, C#, Java, JavaScript (Node + inyección en navegador), Python.

Los nombres CLI principales son cortos (`bazi`, `ziwei`, `horoscope`, `lunar`, `tarot`, `liuyao`). Los alias largos (`mystilink-*`) siguen instalándose por compatibilidad.
La opción `--envelope` envuelve el JSON de la carta como `mystilink.envelope/0.1`.

## Contratos de esquema

| Directorio | Rol |
|-----------|------|
| `mystilink-metaphysics-schema` | JSON Schema compartido para perfiles de nacimiento, base calendárica, sobres y cartas de sistema |

Los repositorios de esquema son paquetes de documentación/contrato. **No** aplican la matriz de lenguajes de las calculadoras (indicado en el README del proyecto).

## MCP local

| Directorio | CLI | Capacidades |
|-----------|-----|--------------|
| `mystilink-mcp` | `mystilink-mcp` | herramientas MCP stdio sobre CLI de calculadoras; FastAPI opcional en bucle local `127.0.0.1` |

Paquete MCP / integración local. **No** aplica la matriz de lenguajes. **No** ofrece un servicio HTTP/HTTPS remoto.

```bash
cd mystilink-mcp && python3 -m pip install -e .
mystilink-mcp status
mystilink-mcp stdio
```

## Agent Skills

| Directorio | Skill `name` | Capacidades |
|-----------|--------------|--------------|
| `mystilink-router-skill` | `mystilink-router` | Elegir un skill de teoría |
| `mystilink-bazi-skill` | `mystilink-bazi` | Scripts de carta BaZi + flujo de lectura |
| `mystilink-ziwei-skill` | `mystilink-ziwei` | Script de carta Zi Wei + flujo de lectura |
| `mystilink-horoscope-skill` | `mystilink-horoscope` | Script de carta natal + flujo de lectura |
| `mystilink-tarot-skill` | `mystilink-tarot` | Script de tirada + flujo de lectura |
| `mystilink-liuyao-skill` | `mystilink-liuyao` | Script de tirada + flujo de lectura |

Los repositorios Skill son paquetes Agent Skill (`SKILL.md` + `scripts/` opcional). **No** aplican la matriz de lenguajes. Instale copiando al directorio de skills del host usando el `name` del skill como nombre de carpeta.

## Inicio rápido (calculadoras)

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

## Inicio rápido (skills)

```bash
cp -R mystilink-bazi-skill /path/to/.cursor/skills/mystilink-bazi
python3 /path/to/.cursor/skills/mystilink-bazi/scripts/bazi_calculate.py --date 1990-05-15 --hour 12
```

## Convenciones compartidas

- Licencia MIT
- README multilingüe con conmutador de idioma en la cabecera
- Calculadoras: matriz C / C++ / C# / Java / JavaScript (Node + navegador) / Python
- CLI de calculadoras: nombres cortos `bazi` / `ziwei` / `horoscope` / `lunar` / `tarot` / `liuyao` (alias largos `mystilink-*` conservados)
- `--envelope` opcional para `mystilink.envelope/0.1`
- Contratos de esquema: JSON Schema + ejemplos; matriz no aplicable
- `mystilink-mcp`: MCP stdio local (+ FastAPI `127.0.0.1` opcional); matriz no aplicable
- Skills: disposición Agent Skill; matriz no aplicable (indicado en cada README de skill)
- No se requieren URL de recursos remotos dentro de los árboles de calculadoras para el cálculo básico
- Las Cursor rules viven bajo `.cursor/rules/` de cada repositorio y de este índice (solo local; no se publican)
