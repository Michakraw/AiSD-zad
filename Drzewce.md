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
