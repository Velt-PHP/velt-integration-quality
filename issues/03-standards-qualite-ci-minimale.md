# Issue 03 - Fixer standards qualite et CI minimale

## Labels

`module:1-foundations`, `area:quality`, `area:ci`, `type:documentation`, `type:tests`, `priority:p0`, `status:ready`

## Objectif

Fixer les standards techniques obligatoires des packages Velt pour eviter que les repos divergent.

## Standards obligatoires Module 1

- PHP 8.2 minimum.
- PSR-4 pour l'autoload.
- PSR-12 pour le style.
- `declare(strict_types=1);` dans les fichiers PHP source.
- PHPUnit pour les tests.
- PHPStan niveau de base, avec montee progressive.
- Composer scripts communs : `test`, `analyse`, `check`.
- GitHub Actions minimale sur push et pull request.
- Conventional Commits recommandes.
- SemVer pour les versions publiques.

## Travail attendu

- Fournir un exemple de scripts Composer communs.
- Fournir un exemple de workflow GitHub Actions.
- Definir le niveau PHPStan initial acceptable.
- Definir ce qui bloque une PR : tests rouges, autoload casse, erreurs fatales.
- Documenter les labels GitHub communs.

## Criteres d'acceptation

- Chaque repo peut lancer `composer test`.
- Chaque repo peut lancer `composer analyse`.
- La CI minimale est copiable dans chaque package.
- Les standards sont comprehensibles par toute l'equipe.

## Definition of Done

- Standards documentes.
- Exemple CI ajoute.
- Checklist PR ajoutee.
- Les sous-modules renvoient vers cette issue pour les standards communs.

