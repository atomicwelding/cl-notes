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

* `M-x count-words` pour compter le nb de lignes/caractères
* `M-g g` pour sauter à une ligne
* `C-/` pour undo
* `C-x <SPACE>` demarrer une selection rectangle
* `C-x r d` delete un rectangle
* `C-x r t` pour écrire sur plusieurs lignes
* `C-c <RET>` pour macroexpand dans un buffer séparé.
* `C-j`, `M-j` pour sauter une ligne (marche dans le REPL notamment).
* `C-c C-d h` look-up dans l'hyperspec.
* `C-x w h` pour highlight un mot. Utiliser unhighlight pour l'enlever.


## Bibliothèques

* cl-who pour générer du html
* cl-pprce pour les regexp
* cl-str pour la manipulation de string (sinon voir uiop)
* parenscript pour générer du javascript
* cl-opengl comme wrapper opengl
* cl-glu/cl-glut
* cepl

## Ressources

* [common-lisp-libraries](https://common-lisp-libraries.readthedocs.io/)
* [cl-cookbook](https://lispcookbook.github.io/)