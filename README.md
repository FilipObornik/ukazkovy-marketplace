# Ukázkový marketplace sdílených skillů

Tohle repo je marketplace se skilly, které fungují ve všech projektech, v Claude i v ChatGPT (Codex). Projektové skilly sem nepatří, ty žijí přímo ve složce projektu.

## Jak je to celé poskládané

```
Firemní Google Drive                    Osobní Google Drive
AI/firma/                               AI/osobni/
├── AGENTS.md          instrukce pro Claude i ChatGPT
├── .agents/skills/    skilly jen pro tento projekt
├── .claude/skills     odkaz na .agents/skills (neupravovat)
├── .claude/settings.json   napojení na tento marketplace (Claude)
└── .codex/config.toml      napojení na tento marketplace (ChatGPT/Codex)

Tento počítač + GitHub
~/AI/ukazkovy-marketplace/  tohle repo = sdílené skilly
└── plugins/sdilene/skills/<nazev>/SKILL.md
```

Pravidlo: **každý skill žije přesně na jednom místě.** Buď ve složce projektu (`.agents/skills`), nebo tady. Nikde jinde, ani v nastavení účtu Claude nebo ChatGPT.

## Co je v pluginu `sdilene`

| Skill | K čemu |
|---|---|
| `novy-skill` | Vytvoří nebo upraví skill a uloží ho na správné místo |
| `publikuj-skilly` | Nahraje změny sdílených skillů na GitHub |
| `kontrola-skillu` | Ukáže, odkud se který skill bere, a najde duplicity |
| `letenka-do-kalendare` | Přepíše letenku nebo jízdenku do kalendáře |

Volání: v Claude `/sdilene:nazev`, v ChatGPT/Codexu `$sdilene:nazev`. Oba nástroje skill spustí i samy, když požadavek odpovídá popisu.

## Běžné situace

- **Chci nový skill**: napiš „ulož to jako skill". AI ho uloží buď jen do projektu (`.agents/skills`), nebo sem mezi sdílené a rovnou publikuje. Když z povahy skillu není jasné, kam patří, zeptá se a doporučí.
- **Upravil jsem sdílený skill ručně**: napiš „publikuj skilly". Bez toho se změna do ostatních nástrojů a zařízení nedostane.
- **Chci převzít skill z druhého projektu**: „podívej se na skill X v projektu Osobní a udělej podle něj verzi pro firmu". Vznikne samostatná kopie, projekty zůstanou nezávislé.
- **Nevím, odkud se skill bere, nebo ho vidím dvakrát**: napiš „zkontroluj skilly".

## Pravidla, která hlídají, aby to fungovalo

- Ve složkách projektů nesmí být soubor `CLAUDE.md`, jinak Claude přestane číst `AGENTS.md`.
- Tohle repo nepatří na Google Drive (Git a Drive se nesnesou), leží jen na počítači a na GitHubu.
- Nové zařízení: nainstalovat `gh`, přihlásit se (`gh auth login`, pak `gh auth setup-git`) a projekty otevřít v Claude i Codexu jako důvěryhodné.
