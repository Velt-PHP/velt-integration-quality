# Issue 04 - Documenter philosophie Velt et decisions ADR

## Labels

`module:1-foundations`, `area:architecture`, `area:documentation`, `type:documentation`, `priority:p1`, `status:ready`

## Objectif

Rendre explicite la philosophie de Velt et conserver les decisions importantes dans des ADR simples.

## Pourquoi cette issue est importante

Le Module 1 expliquait deja comment Velt fonctionne, mais pas assez pourquoi Velt existe. Sans identite claire, le projet peut devenir une copie incomplete de Laravel. Velt doit assumer sa difference : UI declarative PHP, rendu HTML/JSON, preview mobile et composants modulaires.

## Travail attendu

- Ajouter une phrase d'identite officielle.
- Documenter les decisions suivantes :
  - syntaxe PHP declarative plutot que tags custom ;
  - rendu HTML + JSON depuis le meme arbre UI ;
  - packages Composer separes ;
  - Module 1 limite aux fondations, pas aux features applicatives avancees ;
  - events synchrones minimaux en Module 1, events applicatifs complets en Module 4 ;
  - service providers minimaux en Module 1, plugin system complet en Module 6.
- Creer un format ADR court : contexte, decision, consequences.

## Criteres d'acceptation

- Un nouveau membre comprend en cinq minutes pourquoi Velt existe.
- Les decisions structurantes ne sont pas seulement implicites dans les issues.
- Les futures discussions peuvent renvoyer vers un ADR au lieu de rouvrir les memes debats.

## Definition of Done

- Philosophie Velt documentee.
- Format ADR ajoute.
- Au moins quatre ADR initiaux listes.

