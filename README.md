# cl-notes
Mes notes personnelles sur common lisp.


## Table des matières

* [Paredit Cheatsheet](paredit.pdf)
* [Définir un nouveau projet](projet.md)
* [Gestion des erreurs](erreurs.md)

## Définitions

* `:thing` est un symbole placé dans le package `KEYWORD`.
* `#:thing` est un symbole "uninterned", il n'est placé dans aucun package et à chaque fois qu'on l'évalue, un nouveau symbole est créé.

## Raccourcis

* `C-c <RET>` pour macroexpand dans un buffer séparé.
* `C-j` pour sauter une ligne (marche dans le REPL notamment).
* `C-c C-d h` look-up dans l'hyperspec.


## Bibliothèques

* cl-who pour générer du html
* parenscript pour générer du javascript
* cl-opengl comme wrapper opengl
* cl-glu/cl-glut
* cepl

## Ressources

* [common-lisp-libraries](https://common-lisp-libraries.readthedocs.io/)
* [cl-cookbook](https://lispcookbook.github.io/)