---
name: novy-skill
description: Vytvoří nový skill nebo upraví existující a uloží ho na správné místo (projektový do .agents/skills v aktuálním projektu, sdílený do repa marketplace). Použij vždy, když uživatel řekne "ulož to jako skill", "udělej z toho skill", "nový skill", "uprav skill" nebo chce převzít skill z jiného projektu.
---

# Nový nebo upravený skill

Každý skill žije přesně na jednom místě. Tenhle postup zajistí, že skončí na správném.

## 1. Rozhodni, kam skill patří

- **Projektový** (výchozí): používá se jen v tomto projektu. Patří do `<kořen projektu>/.agents/skills/<nazev>/SKILL.md`.
- **Sdílený**: má fungovat ve všech projektech. Patří do repa marketplace (cesta je v `AGENTS.md` projektu, sekce Skilly) do `plugins/sdilene/skills/<nazev>/SKILL.md`.

Když z kontextu není jasné, který typ uživatel chce, zeptej se jednou krátkou otázkou. Když váháš, zvol projektový. Sdílet se vyplatí jen to, co je opravdu stejné všude.

Nikdy neukládej skill do `~/.claude/skills`, `~/.codex/skills`, `~/.agents/skills`, přímo do `.claude/skills` ani do nastavení účtu Claude nebo ChatGPT. Složka `.claude/skills` v projektu je jen odkaz na `.agents/skills`.

## 2. Zkontroluj, jestli už neexistuje

Podívej se do `.agents/skills/` v projektu a do `plugins/sdilene/skills/` v repu marketplace, jestli tam už skill se stejným nebo podobným účelem není. Když ano, uprav ten existující, nevytvářej druhý.

Když uživatel chce převzít skill z jiného projektu, zkopíruj ho sem a uprav pro tento projekt. Neodkazuj na cizí složku, projekty mají zůstat nezávislé.

## 3. Napiš SKILL.md

- **Název složky i `name`**: malá písmena, číslice a pomlčky, bez diakritiky, nejvýš 64 znaků (např. `tydenni-report`).
- **Hlavička**: jen `name` a `description`. Jiná pole nepoužívej, ChatGPT/Codex je ignoruje a skill musí fungovat v obou.
- **`description`**: co skill dělá a kdy se má použít, včetně typických frází uživatele. Podle ní AI pozná, že má skill spustit.
- **Tělo**: postup v krocích, co je vstup, jak má vypadat výstup, případně krátký příklad. Česky, stručně, bez vaty.
- **Pomocné soubory** (šablony, skripty, ukázky) dej do stejné složky vedle `SKILL.md` a odkazuj na ně relativní cestou.

Šablona:

```markdown
---
name: nazev-skillu
description: Co skill dělá. Použij, když uživatel ...
---

# Název skillu

## Postup
1. ...

## Výstup
...
```

## 4. Dokonči

- **Projektový skill** je k dispozici v nové konverzaci v tomto projektu.
- **Sdílený skill** je potřeba publikovat: spusť skill `publikuj-skilly`.

Nakonec uživateli řekni, kde skill leží a jak ho zavolá:
- Claude: `/nazev-skillu` (sdílený `/sdilene:nazev-skillu`)
- ChatGPT/Codex: `$nazev-skillu` (sdílený `$sdilene:nazev-skillu`)

Oba nástroje skill spustí i samy, když požadavek odpovídá popisu.
