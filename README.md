# cl-notes
Mes notes personnelles sur common lisp.

## asdf

Équivalent d'un makefile. Doit être appelé nom-projet.asd Pour définir un système,

```
(asdf:defsystem #:nom-projet
  :description ""
  :author ""
  :license ""
  :version "0.1"
  :serial t ;; permet de load les components à la suite
  :components ((:file "package")
	       (:file "fichier1")))
```

Avant de pouvoir le load, bien vérifier qu'on ait le path dans le registry. Sinon,

```
(push #P"/path/vers/repertoire/" asdf:*central-registry*)
```

Enfin, pour load

```
(asdf:load-system "nom-projet")
```

## defpackage

Doit être appelé package.lisp. Permet d'exposer l'API, de définir les dépendances.


```
(defpackage #:nom-projet
  (:use #:cl) ;; importe les symboles de ces paquets
  (:export #:fonction1
	   #:fonction2))

```