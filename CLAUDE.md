# chef-claude

Deze repo bevat uitsluitend de `recipe-generator` skill (`.claude/skills/recipe-generator/skill.md`) en de gegenereerde output daarvan.

## Wat hier moet gebeuren

- Recepten, profielen en ingrediëntenlijsten worden gegenereerd door de `/recipe-generator` skill — volg altijd die workflow (Fase 0–5) in plaats van losse markdown-bestanden handmatig te verzinnen.
- `recept-profiel.md`, `ingredienten-<maaltijdtype>.md` en `recepten-<maaltijdtype>/` zijn gebruikersoutput van de skill. Behandel ze als brondata: lees ze in plaats van aannames te doen, en wijzig ze alleen via de skill-workflow (of op expliciet verzoek).

## Documentatie

- `README.md` is gebruikersgerichte uitleg (Nederlands) over hoe je deze skill gebruikt — houd die in sync als de skill-workflow wijzigt.
- Geen aparte technische documentatie nodig; de skill zelf is de spec.
