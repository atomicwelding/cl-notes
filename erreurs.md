# Gestion d'erreur

On va prendre l'exemple de la division, facile à comprendre. On retrouve les exemples complets dans le [cl-cookbook](https://lispcookbook.github.io/cl-cookbook/error_handling.html#restarts-interactive-choices-in-the-debugger).



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




