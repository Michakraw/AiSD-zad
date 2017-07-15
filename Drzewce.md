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

