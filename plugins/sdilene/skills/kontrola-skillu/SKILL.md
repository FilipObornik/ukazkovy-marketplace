---
name: kontrola-skillu
description: Zkontroluje nastavení AI složky a skillů. Ukáže, odkud se který skill bere, najde duplicity, ověří odkaz .claude/skills a hlídá, aby nic neblokovalo AGENTS.md. Použij, když uživatel neví, odkud se skill volá, vidí skill dvakrát, skill se chová jinak než čeká, nebo když se ptá, jestli je složka správně nastavená.
---

# Kontrola skillů a složky

## Postup

1. Spusť skript `scripts/kontrola.sh` ze složky tohoto skillu. Jako argument dej kořen aktuálního projektu (složku s `AGENTS.md`):

   ```bash
   bash "<složka tohoto skillu>/scripts/kontrola.sh" "<kořen projektu>"
   ```

2. Výsledek shrň uživateli lidsky a stručně:
   - co je v pořádku,
   - co je potřeba opravit a proč,
   - u duplicit: která kopie je ta správná (projektová v `.agents/skills`, nebo sdílená v pluginu `sdilene`) a které jsou navíc.
3. Nic sám nemaž. Navrhni konkrétní kroky a proveď je až po souhlasu uživatele.

## Jak číst zdroje skillů

| Zdroj ve výpisu | Co to je | Má tam být? |
|---|---|---|
| `projekt` | `.agents/skills` v tomto projektu | Ano, projektové skilly |
| `plugin` | nainstalovaný plugin z marketplace | Ano, sdílené skilly (`sdilene:...`) a oficiální pluginy |
| `claude-uzivatel` | `~/.claude/skills` | Ne, sem skilly nepatří |
| `codex-uzivatel` | `~/.codex/skills` | Ne, sem skilly nepatří |
| `spolecne-uzivatel` | `~/.agents/skills` | Ne, sem skilly nepatří |

Skilly nahrané přímo v nastavení účtu (claude.ai: Nastavení > Skills, ChatGPT: Skills) na disku nejsou. Připomeň uživateli, ať je zkontroluje ručně a duplicitní smaže.
