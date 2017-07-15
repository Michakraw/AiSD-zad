# Drzewce - definicje
[źródło](<https://pl.wikipedia.org/wiki/Drzewiec_(informatyka)>)

Drzewiec = BST + kopiec (w sensie MAX), gdzie w wierzchołku trzymamy dwie informacje:
  - Klucz - dla niego utrzymywana właśność drzewa BST (lewy syn <= ojciec <= prawy syn)
  - Priorytet - dla niego utrzywywana własność kopca (ojciec > lewego i prawego syna)

## Operacje

`search(k)` - `O(log_2(n))` - stosujemy standardowy binarny algorytm wyszukiwania w drzewie binarnych wyszukiwań,
ignorując priorytety. 

`insert(k)` - `O(log_2(n))` - generujemy losowy priorytet `p` dla `k`. Wyszukujemy `k` w drzewcu i tworzymy nowy
wierzchołek jako liść w miejscu, które wskaże binarne przeszukiwanie. Następnie, o ile `k` nie jest
korzeniem i ma większy priorytet niż jego rodzic `r` (a więc zaburzona jest własność kopca),
wykonujemy rotacje pomiędzy `k` i `r`. 

`delete(k)` - `O(log_2(n))`

  - Jeśli `k` jest liściem drzewa, usuwamy go.
  - Jeśli `k` ma jedno dziecko (`h`), usuwamy `k` z drzewa, a z czynimy dzieckiem dotychczasowego
    rodzica dla `k` (lub korzeniem drzewa, jeśli `k` nie miał rodzica).
  - Jeśli `k` ma dwoje dzieci, wybieramy dziecko (`z`) o wyższym priorytecie.
    Następnie rotujemy `z`-`k` tak, żeby dziecko wynieść wyżej. Dzięki temu, że wybraliśmy dziecko
    o wyższym priorytecie, porządek kopcowy zostaje zachowany. Potarzamy operację tak długo,
    aż dojdziemy z wierzchołkiem `k` do któregoś z powyższych przypadków.

Są jeszcze `split` i `merge`, opisane [tutaj](http://informatyka.wroc.pl/node/787?page=0,4).

# Drzewce - zadania

## Zad. 4, cz. 1, 06.2017
Podaj przykład drzewca (tj. podaj wartość klu-
czy wraz z przydzielonymi im priorytetami) o n wierzchołkach, w którym
każdy wierzchołek wewnętrzny ma tylko prawego syna. Następnie podaj,
który wierzchołek będzie wymagał najwięcej rotacji podczas ustawiania
go. Ile to będzie rotacji? Odpowiedź uzasadnij.

### Rozwiązanie

Kolejno wstawiamy (i,j) w kolejności od góry do dołu:

```
(1,n)
  (2,n-1)
    (3,n-2)
      ...
        (n-1,2)
          (n,1)
```

Zero rotacji. Wstawiając element `(m,n-m+1)` w pierwszej części algorytmu wstawiania
do drzewca zachowujemy własność drzewa BST dla klucza (bo `m` jest największym kluczem
w aktualnym drzewie), zaś w drugiej - własność kopca typu max (podobnie, ale to priorytet
jest najmniejszy).

Na pytanie o wierzchołek wymagający najwięcej rotacji możemy spojrzeć też tak.
Weźmy dowolną permutację powyższych insertów. Rozumowanie indukcyjne.

    Baza: Ustawiamy roota.
    Krok: Mamy drzewo o m wierzchołkach, gdzie te wewnętrzne (rozumiane jako `nie będące liściem`)
    posiadają tylko prawego syna. Wykonajmy inserta `m+1` elementu `(k, n-k+1)`. Zgodnie z algorytmem
    wstawiamy go po kluczu (utrzymujemy w końcu właśność BST), rozpatrzmy 2 przypadki:
    1. element `m+1` stał się prawym synem. W efekcie nie mamy zaburzonego drzewca
       (priorytet musi być mniejszy od ojca, bo jest ściśle zależny od klucza)
    2. wpw - lewy syn. Zauważmy, po wykonaniu jednej rotacji w ojcu w prawo uzyskujemy oczekiwany
       drzewiec.

Stąd wynika, że w najgorszym przypadku będziemy mieli co najwyżej jedną rotację per insert.


## Zad. 4, cz. 1, 06.2016
Narysuj ciąg rotacji, które zostaną wykonane w
trakcie wykonywania `delete(p)` na poniższym drzewcu. Litery w wierz-
chołkach drzewca oznaczają klucze, a liczby w nawiasach - priorytety. Ro-
tacje wypisz w kolejności wykonywania.

### Rozwiązanie

Rotujemy w p w lewo:
![1](z40616_1_rotacja_lewo.png)

Rotujemy w p w prawo:
![2](z40616_2_rotacja_prawo.png)

Rotujemy w p w prawo:
![3](z40616_3_rotacja_prawo.png)

p ma jedno dziecko, więc przepinamy:
![4](z40616_4_przepiecie.png)

