# Gestion d'erreur

On va prendre l'exemple de la division, facile à comprendre. On retrouve les exemples complets dans le [cl-cookbook](https://lispcookbook.github.io/cl-cookbook/error_handling.html#restarts-interactive-choices-in-the-debugger).

Une erreur est un type de condition en common lisp.


## Throw une erreur

```
(defun divide (x y)
  (if (equal y 0)
      (error "You can't divide by 0")
      (/ x y)))
```


## Catch les erreurs

```
(defun divide (x y)
  (handler-case (/ x y)
    (error (e)
      (format nil "ERROR : ~a~%" e))))
```


## Créer des restarts


```
(defun divide (x y)
  (restart-case (/ x y)
    (return-zero ()
	:report "Return 0 instead"
      0)
    (divide-by-one ()
      :report "Divide by 1 instead"
      (/ x 1))))
```


## Créer un restart interactif

```
(defun prompt-new-value (prompt) ;; vient du cl-cookbook
  (format *query-io* prompt) ;; *query-io*: the special stream to make user queries.
  (force-output *query-io*)  ;; Ensure the user sees what he types.
  (list (read *query-io*)))  ;; We must return a list.

(defun divide (x y)
  (restart-case (/ x y)
    (redefine-y (value)
      :report "(/ x y) => Redefine a value for y"
      :interactive
        (lambda () (prompt-new-value "Enter a new value for y: "))
      (divide x value))))
```


## Créer une condition



```
(define-condition my-divide-by ()
  ((valeur :initarg :valeur
	   :reader valeur))
  (:report (lambda (condition stream)
	     (format stream "Division by ~a not allowed" (valeur condition))))
  (:documentation "Condition to say we can't divide by a number"))


(make-condition 'my-divide-by :valeur 0)
```


## handler-bind

```
(defun divide (x y)
  (handler-bind
      ((division-by-zero
	 (lambda (condition)
	   (format t "Division par 0 détectée~%")
	   (invoke-restart 'my-continue))))
    (restart-case (/ x y)
      (my-continue ()
	:report "Continuer malgré l'erreur"
	42))))
```



## unwind-protect

```
(defun divide (x y)
  (unwind-protect
       (/ x y)
    (format t "Always evaluated, no matter what happens before")))
```