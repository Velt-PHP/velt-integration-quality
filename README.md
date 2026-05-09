# Sous-module 07 - Integration et qualite

## Mission

Ce sous-module ne represente pas forcement un package Composer runtime. Il sert a stabiliser les bases transversales du Module 1 : integration locale des six repos, standards qualite, tests inter-modules, decisions d'architecture et verification que chaque equipe peut travailler meme si les autres modules ne sont pas termines.

Il existe parce que Velt est decoupe en composants. Sans conventions d'integration, les repos peuvent etre propres individuellement mais impossibles a assembler proprement.

## Perimetre

Inclus :

- strategie Composer `path repositories` pour developper les packages localement ;
- matrice de tests unitaires, contract tests et tests d'integration ;
- conventions PSR-4, PSR-12, `strict_types=1`, PHPUnit, PHPStan ;
- squelette de GitHub Actions commun ;
- decisions d'architecture a documenter sous forme d'ADR ;
- verification des dependances autorisees entre modules ;
- methode de test avec fakes/stubs quand un module dependant n'est pas pret.

Exclus :

- publication Packagist officielle ;
- release automation complete ;
- plugin system avance ;
- observabilite production ;
- audit de securite production complet.

## Comment tester meme sans les dependances completes

Chaque package doit pouvoir etre teste de trois manieres.

1. Tests unitaires purs : le package teste ses classes avec des fakes locaux. Par exemple `veltphp/http` teste son router avec un faux container au lieu d'attendre le kernel complet.
2. Contract tests : le package verifie qu'il respecte les interfaces publiques du kernel. Par exemple une fausse `ResponseInterface` suffit pour tester la normalisation HTTP.
3. Tests d'integration locaux : un dossier sandbox installe les packages via Composer `path repositories` pour verifier les flux `route -> page -> html` et `preview -> page -> json`.

Les equipes ne doivent pas attendre que tous les modules soient finis pour tester. Si un module dependant manque, elles creent un fake conforme au contrat public, puis remplacent ce fake par le vrai package dans les tests d'integration.

## Issues

- [Issue 01 - Definir Composer path repositories inter-modules](issues/01-composer-path-repositories-inter-modules.md)
- [Issue 02 - Creer matrice de tests inter-modules](issues/02-matrice-tests-inter-modules.md)
- [Issue 03 - Fixer standards qualite et CI minimale](issues/03-standards-qualite-ci-minimale.md)
- [Issue 04 - Documenter philosophie Velt et decisions ADR](issues/04-philosophie-velt-decisions-adr.md)

