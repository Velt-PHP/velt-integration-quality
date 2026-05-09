# Issue 01 - Definir Composer path repositories inter-modules

## Labels

`module:1-foundations`, `area:integration`, `area:composer`, `type:architecture`, `type:documentation`, `priority:p0`, `status:ready`

## Objectif

Permettre aux six repos du Module 1 de se parler en local avant publication Packagist, sans copier de code et sans chemins absolus fragiles.

## Pourquoi cette issue est obligatoire

Velt utilise plusieurs repos : `veltphp/kernel`, `veltphp/http`, `veltphp/ui`, `veltphp/database`, `veltphp/cli` et `veltphp/preview`. Pendant le developpement, ces packages ne seront pas encore publies. Composer doit donc les relier via `path repositories`.

Sans cette convention, chaque equipe risque de tester avec une copie locale differente et les integrations casseront au dernier moment.

## Travail attendu

- Documenter un exemple de `composer.json` sandbox avec `repositories` de type `path`.
- Utiliser des chemins relatifs, par exemple `../veltphp-kernel`.
- Definir les noms Composer officiels : `veltphp/kernel`, `veltphp/http`, `veltphp/ui`, `veltphp/database`, `veltphp/cli`, `veltphp/preview`.
- Expliquer quand utiliser `"symlink": true` pendant le developpement.
- Ajouter une commande de verification : `composer install` puis `composer dump-autoload`.
- Documenter comment detecter une dependance circulaire.

## Exemple cible

```json
{
  "repositories": [
    { "type": "path", "url": "../veltphp-kernel", "options": { "symlink": true } },
    { "type": "path", "url": "../veltphp-http", "options": { "symlink": true } },
    { "type": "path", "url": "../velt-ui", "options": { "symlink": true } }
  ],
  "require": {
    "veltphp/kernel": "*",
    "veltphp/http": "*",
    "veltphp/ui": "*"
  }
}
```

## Criteres d'acceptation

- Une sandbox peut installer les packages locaux via Composer.
- Les namespaces PSR-4 sont resolus sans copie manuelle.
- La documentation explique le workflow Windows, Linux et macOS.
- Les chemins absolus sont interdits dans les exemples officiels.

## Definition of Done

- Convention Composer documentee.
- Exemple JSON valide ajoute.
- Verification locale de l'autoload decrite.
- Les README des sous-modules pointent vers cette convention.

