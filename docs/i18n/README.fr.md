# Index des bibliothèques Mystilink

> Languages: [English](../../README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Français](README.fr.md) | [Español](README.es.md)

## Aperçu

Index des bibliothèques de calcul Mystilink, des contrats de schéma, de l’intégration MCP locale et des paquets Agent Skill. Chaque projet est un dépôt indépendant sous cette racine. Installation et exécution : voir le README de chaque projet.

## Calculateurs

| Répertoire | CLI | Capacités |
|-----------|-----|--------------|
| `mystilink-lunar-calendar` | `lunar` | Grégorien↔lunaire, mois intercalaires, ganzhi/zodiaque annuel, JSON |
| `mystilink-bazi-calculator` | `bazi` | Quatre Piliers (BaZi), DaYun, LiuNian |
| `mystilink-ziwei-calculator` | `ziwei` | Thème Zi Wei Dou Shu |
| `mystilink-horoscope-calculator` | `horoscope` | Natal, transit journalier, transit mensuel |
| `mystilink-tarot-calculator` | `tarot` | Tirage RWS (écarts, droit/renversé) |
| `mystilink-liuyao-calculator` | `liuyao` | Tirage à six lignes (ben/zhi) |

Les dépôts calculateurs suivent la matrice de langages : C, C++, C#, Java, JavaScript (Node + injection navigateur), Python.

Les noms CLI principaux sont courts (`bazi`, `ziwei`, `horoscope`, `lunar`, `tarot`, `liuyao`). Les alias longs (`mystilink-*`) restent installés pour compatibilité.
L’option `--envelope` enveloppe le JSON du thème en `mystilink.envelope/0.1`.

## Contrats de schéma

| Répertoire | Rôle |
|-----------|------|
| `mystilink-metaphysics-schema` | JSON Schema partagé pour profils de naissance, base calendaire, enveloppes et thèmes système |

Les dépôts de schéma sont des paquets documentation/contrat. Ils n’appliquent **pas** la matrice de langages des calculateurs (indiqué dans le README du projet).

## MCP local

| Répertoire | CLI | Capacités |
|-----------|-----|--------------|
| `mystilink-mcp` | `mystilink-mcp` | outils MCP stdio sur les CLI calculateurs ; FastAPI loopback optionnel sur `127.0.0.1` |

Paquet MCP / intégration locale. N’applique **pas** la matrice de langages. Ne fournit **pas** de service HTTP/HTTPS distant.

```bash
cd mystilink-mcp && python3 -m pip install -e .
mystilink-mcp status
mystilink-mcp stdio
```

## Agent Skills

| Répertoire | Skill `name` | Capacités |
|-----------|--------------|--------------|
| `mystilink-router-skill` | `mystilink-router` | Choisir un skill de théorie |
| `mystilink-bazi-skill` | `mystilink-bazi` | Scripts BaZi + flux de lecture |
| `mystilink-ziwei-skill` | `mystilink-ziwei` | Script thème Zi Wei + flux de lecture |
| `mystilink-horoscope-skill` | `mystilink-horoscope` | Script thème natal + flux de lecture |
| `mystilink-tarot-skill` | `mystilink-tarot` | Script de tirage + flux de lecture |
| `mystilink-liuyao-skill` | `mystilink-liuyao` | Script de tirage + flux de lecture |

Les dépôts Skill sont des paquets Agent Skill (`SKILL.md` + `scripts/` optionnel). Ils n’appliquent **pas** la matrice de langages. Installation : copier dans le répertoire skills de l’hôte en utilisant le `name` du skill comme nom de dossier.

## Démarrage rapide (calculateurs)

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

## Démarrage rapide (skills)

```bash
cp -R mystilink-bazi-skill /path/to/.cursor/skills/mystilink-bazi
python3 /path/to/.cursor/skills/mystilink-bazi/scripts/bazi_calculate.py --date 1990-05-15 --hour 12
```

## Conventions partagées

- Licence MIT
- README multilingue avec bascule de langue en en-tête
- Calculateurs : matrice C / C++ / C# / Java / JavaScript (Node + navigateur) / Python
- CLI calculateurs : noms courts `bazi` / `ziwei` / `horoscope` / `lunar` / `tarot` / `liuyao` (alias longs `mystilink-*` conservés)
- `--envelope` optionnel pour `mystilink.envelope/0.1`
- Contrats de schéma : JSON Schema + exemples ; matrice non applicable
- `mystilink-mcp` : MCP stdio local (+ FastAPI `127.0.0.1` optionnel) ; matrice non applicable
- Skills : disposition Agent Skill ; matrice non applicable (indiqué dans chaque README skill)
- Aucune URL de ressource distante requise dans les arbres calculateurs pour le calcul de base
- Les Cursor rules vivent sous `.cursor/rules/` de chaque dépôt et de cet index (local uniquement ; non publiées)
