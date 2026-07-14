# design-polish-skills

Skill dla agentów kodujących (Claude Code, Cursor, Codex, OpenCode i inne wspierane przez ekosystem [Agent Skills](https://agentskills.io)), który automatyzuje "design pass" po pierwszej iteracji UI: audytuje istniejący interfejs względem pliku `DESIGN.MD` (traktowanego jako standard/source of truth projektu), dopytuje o wszystko, czego `DESIGN.MD` nie pokrywa, wprowadza styl bez zmiany layoutu, i na końcu aktualizuje `DESIGN.MD` tak, żeby zawsze pozostawał kompletnym standardem.

## Install

```
npx skills add emblemo/design-polish-skills
```

Instalacja tylko jednego skilla (jeśli w repo pojawi się ich więcej w przyszłości):

```
npx skills add emblemo/design-polish-skills --skill design-polish
```

Do konkretnego agenta:

```
npx skills add emblemo/design-polish-skills -a claude-code
```

Globalnie (dostępny we wszystkich projektach zamiast tylko w bieżącym):

```
npx skills add emblemo/design-polish-skills -g
```

## Reference

- **[design-polish](skills/design-polish/SKILL.md)** — audytuje UI względem `DESIGN.MD`, dopytuje o braki/konflikty, stosuje styl bez ruszania layoutu, aktualizuje `DESIGN.MD` po zakończeniu.
  - `templates/DESIGN.baseline.md` — bazowy, monochromatyczny `DESIGN.MD` (dark-only) używany, gdy w projekcie nie ma jeszcze własnego standardu.

## Jak to działa

Odpalasz frazą typu "dostyluj UI", "zrób design pass", "ujednolić styl w projekcie" — albo agent sam to zaproponuje, gdy wspomnisz o kończeniu pierwszej iteracji projektu z gotowym UI.

Skill zawsze najpierw sprawdza, czy w projekcie jest `DESIGN.MD`:
- jeśli tak — traktuje go jako standard i audytuje UI względem niego,
- jeśli nie — pyta, czy chcesz bazowy szablon (`templates/DESIGN.baseline.md`) czy `DESIGN.MD` wygenerowany z analizy istniejącego kodu.

Żadna zmiana stylistyczna nie wchodzi w życie bez dopytania Cię o przypadki, których `DESIGN.MD` nie pokrywa.

## Update

```
npx skills update design-polish
```

## License

MIT
