# Issue 02 - Creer matrice de tests inter-modules

## Labels

`module:1-foundations`, `area:integration`, `area:tests`, `type:tests`, `type:architecture`, `priority:p0`, `status:ready`

## Objectif

Definir comment chaque sous-module se teste seul et comment les flux critiques du Module 1 se testent ensemble.

## Travail attendu

- Lister les tests unitaires obligatoires par package.
- Lister les contract tests obligatoires contre les interfaces du kernel.
- Lister les tests d'integration minimum :
  - `route -> controller -> Page -> HTML Response` ;
  - `preview session -> Page -> JSON Response` ;
  - `CLI make:feature -> fichiers generes -> autoload Composer` ;
  - `database config -> PDO SQLite -> requete preparee`.
- Definir comment utiliser des fakes quand un module dependant n'est pas disponible.
- Definir une sandbox `tests/integration` ou un repo d'assemblage temporaire.

## Criteres d'acceptation

- Chaque equipe sait quoi tester avant que les autres modules soient termines.
- Les tests d'integration ne dependent pas d'une base MySQL externe.
- SQLite en memoire est la base officielle des tests database Module 1.
- Les erreurs JSON et HTML sont testees separement.

## Definition of Done

- Matrice de tests documentee.
- Fakes/stubs recommandes documentes.
- Deux flux bout-en-bout minimum sont decrits.
- Les criteres de fin du Module 1 s'appuient sur cette matrice.

