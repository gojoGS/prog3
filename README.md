# Magas szintű prgramozási nyelvek 3 mintafeladatok

1. Definiálja azt a függvényt, amely paraméterként megkap egy pozitív egész számot (n-et), és előálltja
azt a listát, amely a Fibonacci-sorozat azon elemeit tartalmazza, amelyeknek az értéke nem haladja
meg n-et!

    ```racket
    (define (fibonacci-range n [fib 1] [fib-prev 0])
      (if (> (+ fib fib-prev) n)
          (cons fib-prev (cons fib '()))
          (cons fib-prev (fibonacci-range n (+ fib fib-prev) fib))))
    ```

1. Adja meg azt a kifejezést, amely egy egész számokat tartalmazó listából előállítja azt a listát, amely az
eredeti listának csak a páros értékű elemeit tartalmazza!

    ```racket
    (filter (lambda (x) (even? x)) '(1 2 3 4 5))
    ```

1. Adja meg azt a kifejezést, amely kiszámítja a Fibonacci-sorozat azon páros értékű elemeinek az
összegét, amelyeknek az értéke nem haladja meg a négymilliót!

    ```racket
    (apply + (filter even? (fibonacci-range 4000000)))
    ```

1. Definiálja azt a függvényt, amely paraméterként megkap egy pozitív egész számot (n-et), és amely
eredményül azt a legkisebb pozitív egész számot adja, amely 1-től n-ig minden egész számmal
maradék nélkül osztható! Vigyázzon, ez a szám nem minden esetben azonos n! értékével!

    ```racket
    (define (genius lst)
      (apply lcm lst))
    ```

1. Definiálja azt a függvényt, amely paraméterként megkap egy pozitív egész számot (n-et), és amely
kiszámítja az első n pozitív egész szám összegének négyzetét, valamint az első n pozitív egész szám
négyzeteinek összegét, és eredményül e két érték ebben a sorrendben vett különbségét adja!

    ```racket
    (define (difference n)
      (define (iota n)
        (range 1 (add1 n)))
      (define (square-sum lst)
        (sqr (foldl + 0 lst)))
      (define (sum-squares lst)
        (foldl + 0 (map sqr lst)))
      (let ([nums (iota n)])
        (- (square-sum nums) (sum-squares nums))))
    ```

1. Definiálja azt a predikátumot, amely a paraméterként megkapott, egész számokat tartalmazó listáról
eldönti, hogy annak elemei monoton csökkenő sorozatot alkotnak-e! Ha igen, akkor a függvény #t
értéket, ellenkezdő esetben #f értéket adjon eredményül!

    ```racket
    (define (decreasing lst)
      (define (drop-last lst) (reverse (cdr (reverse lst))))
      (andmap (λ (x) (not (negative? x))) (map - (drop-last lst) (cdr lst))))
    ```

    ```racket
    (define (decreasing lst)
      (cond
        [(empty? (cdr lst)) #t]
        [(>= (car lst) (cadr lst)) (decreasing (cdr lst))]
        [else #f]))
    ```


1. Definiálja azt a függvényt, amely paraméterként megkap egy pozitív egész számot (n-et), és előállítja
a szám számjegyeiből képzett listát!

    ```racket
    (define (number->list n)
      (map string->number (map string (string->list(number->string n)))))
    ```

1. Definiálja azt a függvényt, amely meghatározza egy tetszőleges, egész számokat tartalmazó lista
elemeinek az összegét!

    ```racket
    (define (sum lst)
      (foldl + 0 lst))
    ```

1. 2<sup>15</sup> = 32768, az eredmény számjegyeinek összege pedig 3 + 2 + 7 + 6 + 8 = 26. Definiálja azt a
függvényt, amely paraméterként megkap egy nemnegatív egész számot (n-et), és meghatározza 2<sup>n</sup>
számjegyeinek az összegét!

    ```racket
    (define (get-sum-power n)
      (foldl + 0(map string->number(map string(string->list(number->string(expt 2 n)))))))
    ```

1. Definiálja azt a függvényt, amely paraméterként megkap egy pozitív egész számot (n-et), és előállítja
azoknak a pozitív számoknak a listáját, amelyek kisebbek n-nél és maradék nélkül osztják n-et!

    ```racket
    (define (fancy-schmancy n [curr (sub1 n)] [divisors '()])
      (if (< curr 1)
          divisors
          (if (integer? (/ n curr))
              (fancy-schmancy n (sub1 curr) (cons curr divisors))
              (fancy-schmancy n (sub1 curr) divisors))))
    ```

    **Megj: ez csak egy nagyon fancy megfogalmazása annak, hogy adja vissza a fv n osztóinak listáját**

1. Definiálja azt a predikátumot, amely paraméterként megkap két pozitív egész számot (n-et és m-et),
és eldönti róluk, hogy barátságos számok-e! Az n és m számokat barátságosnak nevezünk, ha az n
összes nála kisebb osztóinak összege megegyezik m-mel, míg az m összes nála kisebb osztóinak
összege egyenlő n-nel! Barátságos számok például a 220 és a 284, mert 220 osztóinak összege `(1 + 2+ 4 + 5 + 10 + 11 + 20 + 22 + 44 + 55 + 110)` éppen 284, míg 284 osztóinak összege `(1 + 2 + 4 + 71 + 142)` éppen 220. A predikátum értéke #t legyen, ha n és m barátságos számok, egyébként pedig #f!

    ```racket
    (define (friendly n m)
      (define (sum-of-divisors n)
        (foldl + 0 (filter (λ (x) (integer? (/ n x))) (range 1 n))))
      (and (= n (sum-of-divisors m))
           (= m (sum-of-divisors n))))
    ```

1. Definiálja azt a predikátumot, amely a paraméterként megkapott, egész számokat tartalmazó listáról
eldönti, hogy annak minden eleme azonos-e! Ha igen, akkor a predikátum #t értéket, ellenkezdő
esetben #f értéket adjon eredményül!

    ```racket
    (define (just-uniq lst)
      (empty? (remove* (list (car lst)) lst)))
    ```

1. Definiáljon azt a függvényt, amely paraméterként megkap egy listát, amely azt tartalmazza, hogy
milyen magasak az utcában az egymás mellett álló házak. Az utca elrendezését elfogadhatónak
nevezzük, ha az egymás mellett álló házak magasságkülönbsége pontosan 1. A függvény #t értéket
adjon vissza, ha a házak elrendezése a paraméterként megadott listában elfogadható, egyébként
pedig #f értéket szolgáltasson!

    ```racket
    (define (house lst)
      (for/and ([a lst]
                (b (cdr lst)))
        (= 1 (abs (- a b)))))
    ```

1. Definiálja azt a függvényt, amely paraméterként megkap egy ládaszámot, egy láda kapacitását,
valamint egy listát, amely azt tartalmazza, hogy a kert almafái hány kilogramm almát teremnek. A
függvény adja meg, hogy hány ládát kell felhasználni az almák betakarításához, ha a lehető legtöbb
ládát szeretnénk telepakolni! Ha nincs elegendő láda az almák betakarításához, a függvény egy ennek
megfelelő szöveget adjon vissza!

    ```racket
    #lang racket

    (define (eva n cap lst)
      (let ([apples (foldl + 0 lst)])
        (if (> apples (* n cap))
            "Fock off ye bloody wanker"
            (ceiling (/ apples cap)))))

    ```

1. Definiálja azt a függvényt, amely paraméterként megkap egy számot, amely a módosított Collatz-
sorozat kezdőszáma lesz majd, és visszaadja az ezzel a számmal kezdődő módosított
elemszámát. A sorozat annyiban tér el az eredeti Collatz-sorozat definíciójától, hogy amennyiben a
sorozat adott eleme osztható 3-mal, akkor megtörténik az osztás.

    ```racket
    (define (elem-collatz n)
      (define (mod-collatz n [elem 0])
        (cond
          [(= 1 n) '()]
          [(even? n) (cons n (mod-collatz (/ n 2) (add1 elem)))]
          [(integer? (/ n 3)) (cons n (mod-collatz (/ n 3) (add1 elem)))]
          [else (cons n (mod-collatz (add1 (* 3 n)) (add1 elem)))]))
      (length (mod-collatz n)))
    ```

1. Definiálja azt a függvényt, amely az eredeti Collatz-sorozatot egy kezdő n értéktől elindítva
meghatározza a sorozat előállítása során kapott legnagyobb szám értékét!

    ```racket
    (define (max-collatz n)
      (define (collatz n)
        (cond
          [(= 1 n) '(1)]
          [(even? n) (cons n (collatz (/ n 2)))]
          [else (cons n (collatz (add1 (* 3 n))))]))
      (foldl max n (collatz n)))
    ```

1. Definiálja azt a függvényt, amely a paramétereként megadott listáról eldönti, hogy az elemei
maximálisan milyen mélységben vannak egymásba ágyazva! Néhány példa egyszintű listára: '(), '(1),
'(1 2 3 4 5). Kétszintű lista például: '((1) 2), '(1 (2)), '((1)), '(1 (2 3)), '(1 (2) 3). Háromszintű lista: '(((1) 2)
3).

    ```racket
    (define (depth lst [maxd 0])
      (define (atom? x)
        (and (not (null? x))
             (not (pair? x))))
      (match lst
        [(list) (add1 maxd)]
        [(list a) (if (atom? a)
                      (add1 maxd)
                      (depth a (add1 maxd)))]
        [(list a b ...) (if (atom? a)
                            (depth b maxd)
                            (max (depth a (add1 maxd))
                                 (depth b maxd)))]
        [_ maxd]))
    ```

    ```racket
    (define (list-depth lst [depth 1])
      (cond [(null? lst) depth]
            [(not (list? (car lst))) (list-depth (cdr lst) depth)]
            (else (max (list-depth (car lst) (+ 1 depth))
                       (list-depth (cdr lst) depth)))))
    ```

1. Definiálja azt a függvényt, amely elemi listaműveletek segítségével (a beépített rendező függvények
használata nélkül) beszúr egy paraméterként megadott egész számot egy szintén paraméterként
megadott, egész számokat tartalmazó, nagyság szerint növekvő sorrendbe rendezett listába, és
eredményül a bővített, szintén nagyság szerint növekvő sorrendbe rendezett listát adja!

    ```racket
    (define (insert n lst)
      (cond
        [(empty? lst) (list n)]
        [(<= n (car lst)) (cons n lst)]
        [else (cons (car lst) (insert n (cdr lst)))]))
    ```

1. Definiálja azt a függvényt, amely elemi listaműveletek segítségével (a beépített rendező függvények
használata nélkül) nagyság szerint növekvő sorrendbe rendezi a paraméterként megkapott, egész
számokat tartalmazó lista elemeit, és eredményül a rendezett listát adja!

    ```racket
    (define (sorted-helper-helper n sorted)
      (cond
        [(empty? sorted) (list n)]
        [else (cond
                [(<= n (car sorted)) (cons n sorted)]
                [else (cons  (car sorted) (sorted-helper-helper n (cdr sorted)))])]))

    (define (sorted-helper lst sorted)
      (cond
        [(empty? lst) sorted]
        [else (sorted-helper (cdr lst) (sorted-helper-helper (car lst) sorted))]))

    (define (sorted lst)
      (sorted-helper lst '()))
    ```

1. Definiálja azt a függvényt, amely paraméterként kap
   1. egy B egész számot, a repülőgépjegyek alapárát,
   1. egy D egész számot, a jegyek drágulásának az értékét (minden jegy D-vel kerül többe, mint az
előző),
   1. egy W egész számot, az ablak mellé szóló jegyek (A és F oszlop) felárát,
   1. egy L egész számot, a nagy lábterű (vészkijárati) sorokba szóló helyek felárát,
   1. egy listát, amely a nagy lábterű (vészkijárati) sorok sorszámait tartalmazza), valamint
   1. egy listát, amely a helyfoglalásokat tartalmazza (sor, betűjel) formában.

    Például:

    `(foo 20000 700 2000 5000 '(1 2 17 18) '((23 #\A) (35 #\B) (1 #\A) (1 #\C) (5 #\E)))`

    A függvény számítsa ki és adja vissza az eladott jegyek összértékét, feltételezve, hogy a jegyek árait a
helyfoglalások sorrendjében határozzuk meg!

    ```racket
    (define (röpcsi alap dragasag a-f-felar bigfoot-felar lst-bigfoot lst-helyek)
      (let* ([emberek (length lst-helyek)]
             [alap-sum (* alap emberek)]
             [dragasag-sum (* dragasag (foldl + 0 (range emberek)))]
             [bigfoot-sum (* bigfoot-felar (length (filter (λ (x) (list? x))
                                                           (map (λ (x) (member (second x)
                                                                               lst-bigfoot))
                                                                lst-helyek))))]
             [a-f-sum (* a-f-felar (length (filter (λ (x) (list? x))
                                                           (map (λ (x) (member (first x)
                                                                               '(#\A #\F)))
                                                                lst-helyek))))])
        (foldl + 0 (list alap-sum dragasag-sum bigfoot-sum a-f-sum))))
    ```

1. Definiálja azt a függvényt, amely a paramétereként megadott n pozitív egész számnak meghatározza
az összes pozitív egész osztóját! A megoldáshoz elemi aritmetikai és listakezelő függvényeket
használjon, ne használja az erre a célra megírt beépített függvény(eke)t!

    ```racket
    (define (divisors n [div n])
      (cond
        [(= div 0) '()]
        [(zero? (remainder n div)) (cons div (divisors n (- div 1)))]
        [else (divisors n (- div 1))]))
    ```

1. Definiálja azt a függvényt, amely a paramétereként megadott pozitív egész számot évszámnak
tekintve meghatározza, hogy az adott év szökőév-e! Szökőévek azok az évek, amelyek 4-gyel osztva 0
maradékot adnak, kivéve azokat a 100-zal oszthatókat, amelyek 400-as maradéka nem 0. Így szökőév
1996, 2000, 2004, 2008, 2012, de nem szökőév 1900 és 2100.

    ```racket
    (define (leap-year? y)
      (and (zero? (modulo y 4)) (or (positive? (modulo y 100)) (zero? (modulo y 400)))))
    ```

1. Definiálja azt a függvényt, amely a paraméterként megadott hónap és nap sorszáma alapján
meghatározza, hogy az adott hónap adott napja hányadik nap az évben! Feltételezheti, hogy a
vizsgált év nem szökőév. Például január 1-je az éve első napja, december 31-e pedig a 365-dik.

    ```racket
    (define (dody m d [ord 0] [curr-m 1])
      (define (m-length mm)
        (cond
          [(= mm 2) 28]
          [(member mm '(1 3 5 7 8 10 12)) 31]
          [else 30]))
      (if (= m curr-m)
          (+ d ord)
          (dody m d (+ ord (m-length curr-m)) (add1 curr-m))))
    ```

1. Definiálja azt a függvényt, amely bővíti a paraméterként megadott elemmel a szintén paraméterként
megadott listát az ugyancsak paraméterként megadott pozíción! A listaelemek pozícióinak számozása
0-tól induljon! Amennyiben a listának nincsen annyi eleme, mint a megadott pozíció, az eredeti lista
legyen a függvény visszatérési értéke!

    ```racket
    (define (insert val lst pos)
      (cond
        [(null? lst) '()]
        [(= pos 0) (cons val lst)]
        [else (cons (car lst) (insert val (cdr lst) (sub1 pos)))]))
    ```

1. Definiálja azt a predikátumot, amely meghatározza, hogy egy lista palindróm-e, azaz az elemeinek az
értékei hátulról előrefelé haladva megegyeznek az eredeti sorrendben vett értékekkel!

    ```racket
    (define (palindrome? lst)
      (empty? (remove* '(#t) (map equal? lst (reverse lst)))))
    ```

    ```racket
    (define (palindrome? lst)   
      (andmap equal? lst (reverse lst)))
    ```

1. Definiálja azt a függvényt, amely összefésüléses rendezéssel a két, paramétereként megadott, egész
számokat növekvő sorrendben tartalmazó listát összefésüli, és a rendezett listát adja eredményül!

    ```racket
    (define (merge-list lst1 lst2)
      (cond [(empty? lst1) lst2]   
            [(empty? lst2) lst1]   
            [(<= (car lst1) (car lst2))
                 (cons
                  (car lst1)
                  (merge-list (cdr lst1) lst2))]
            [else (cons
                   (car lst2)
                   (merge-list lst1 (cdr lst2)))]))
    ```
