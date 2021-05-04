# Függvények Iminek

- [Függvények Iminek](#függvények-iminek)
  - [`cons`](#cons)
  - [`filter`](#filter)
  - [`apply`](#apply)
  - [`lcm`](#lcm)
  - [`range`](#range)
  - [`foldl`](#foldl)
  - [`map`](#map)
  - [`let`](#let)
  - [`andmap`](#andmap)
  - [`cond`](#cond)
  - [`string->` stb..](#string--stb)
  - [`for`, és társai](#for-és-társai)

## `cons`

Cuccokat rak le a lista elejére

```lisp
(cons 4 '(1 2 3))
; -->> '(4 1 2 3)
```

## `filter`

Kiszedi a listából azokat, amikre a függvény (pl.: `even?`) igaz.

```lisp
(filter even? '(1 2 3 3 4 5 6 7))
; -->> '(2 4 6)
```
## `apply`

Egy függvényt alkalmaz egy listára

```lisp
(apply + '(1 2 3))
; -->> 6 = 1 + 2 + 3
; ekvivalens ezzel:
(+ 1 2 3)
```

## `lcm`

Legkisebb közös többszörös.

## `range`

```lisp
(range 5)
; -->> '(0 1 2 3 4)
(range 2 5)
; -->> '(2 3 4)
```

## `foldl`

```lisp
(foldl - 0 '(1 2 3))
;(- 3 (- 2 (- 1 0)))
```

## `map`

```lisp
(map add1 '(1 2 3))
; -->> '(2 3 4)
```

## `let`

"Változókat" deklarál

```lisp
(define (foo lst)
  (let ([elso (car lst)]
        [masodik (car (cdr lst))])
    (+ elso masodik)))
```

## `andmap`

Egy függvényt alkalmazva a lista minden elemére, minden esetben igazat ad e vissza.

```lisp
(andmap even? '(2 3 4 5 6))
; -->> #f
```

## `cond`

Összetett if + else if + ... + else, egyben.

```lisp
(define (foo lst)
  (cond
    [(empty? lst) (apply + lst)]
    [(= 0 (car lst)) 1]
    [(= 1 (car lst)) 0]
    [else (apply + (cdr lst))]))
```

## `string->` stb..

```lisp
(number->string 1024)
; -->> "1024"
(string->list "1024")
; -->> '(#\1 #\0 #\2 #\4)
(string->number "1024")
; -->> 1024
```

## `for`, és társai

For ciklus, a rangek közül mindig a rövidebb

```lisp
(for ([i '(1 2 3 4)]
        [j '(-1 -2 -3)])
    (display(* i j)))
; kiírja hogy -1-4-9
```

```lisp
(for/and ([i '(1 2 3 4)]
        [j '(-1 -2 -3)])
   (even? (* i j)))
; -->> #f
```

```lisp
(for/list ([i '(1 2 3 4)]
        [j '(-1 -2 -3)])
   (* i j))
; -->> '(-1 -4 -9)
```
<!-- 
## ``

```lisp

```

## ``

```lisp

```

## ``

```lisp

```

## ``

```lisp

```

## ``

```lisp

```

## ``

```lisp

```

## ``

```lisp

``` -->