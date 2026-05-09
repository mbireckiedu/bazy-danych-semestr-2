# Ćwiczenie 3  SQL (SUBQUERY, EXISTS, CASE)

---

## Uruchomienie środowiska

W ćwiczeniu korzystamy z tej samej bazy danych co w ćwiczeniach nr 1 i 2.

### Jeśli masz już środowisko:

```bash
docker compose up -d
```

### Jeśli coś nie działa:

```bash
docker compose down -v
docker compose up -d
```

### Jeśli nie masz środowiska

Wróć do instrukcji z ćwiczenia nr 1 i wykonaj:

* uruchomienie Dockera,
* start serwera MySQL,
* wykonanie skryptów SQL tworzących bazę danych i wypełniających ją przykładowymi danymi.

---

## Punktacja

Do zdobycia: **10 punktów**

* Zadania 1–5: po **2 pkt**
* Zadanie 6: **BONUS 2 pkt**

### Skala ocen

* 0–4.5 pkt → 2.0
* 5–5.5 pkt → 3.0
* 6–6.5 pkt → 3.5
* 7–8 pkt → 4.0
* 8.5–9 pkt → 4.5
* 9.5–10 pkt → 5.0

---

# Zadania

---

## Zadanie 1 (2 pkt)

Znajdź użytkowników, którzy mają przynajmniej jedno zamówienie.

---

## Zadanie 2 (2 pkt)

Znajdź użytkowników, którzy nie mają żadnych zamówień.

---

## Zadanie 3 (2 pkt)

Znajdź zamówienia, których wartość jest większa niż średnia wartość wszystkich zamówień.

---

## Zadanie 4 (2 pkt)

Znajdź leki, których cena w którejkolwiek pozycji zamówienia jest wyższa niż średnia cena wszystkich pozycji zamówień.

Zwróć:

* `drg_id`,
* nazwę leku,
* cenę pozycji (`ori_price`),
* średnią cenę wszystkich pozycji.

---

## Zadanie 5 (2 pkt)

Dla każdego zamówienia wyświetl:

* `ord_id`,
* wartość zamówienia,
* informację:

  * `DUŻE` — jeśli wartość zamówienia jest większa niż 100,
  * `MAŁE` — w przeciwnym przypadku.

Użyj instrukcji `CASE`.

---

## Zadanie 6 (BONUS 2 pkt)

Znajdź użytkowników, którzy złożyli zamówienie zawierające więcej niż jeden rodzaj leku.

---

## Zasady oddania

* plik `.sql` z rozwiązaniami,
* numeracja zgodna z numeracją zadań,
* zrzuty ekranu z wynikami,
* commit plików do repozytorium.

---

# Wskazówki

---

## Podzapytanie (Subquery)

```sql
SELECT *
FROM tabela
WHERE kolumna IN (
    SELECT kolumna
    FROM inna_tabela
);
```

Podzapytanie pozwala wykorzystać wynik jednego zapytania wewnątrz innego zapytania.

---

## EXISTS

```sql
SELECT *
FROM user u
WHERE EXISTS (
    SELECT 1
    FROM `order` o
    WHERE o.ord_usr_id = u.usr_id
);
```

`EXISTS` sprawdza, czy istnieje przynajmniej jeden pasujący rekord.

---

## NOT EXISTS

```sql
SELECT *
FROM user u
WHERE NOT EXISTS (
    SELECT 1
    FROM `order` o
    WHERE o.ord_usr_id = u.usr_id
);
```

`NOT EXISTS` wybiera rekordy, dla których nie istnieje żadne dopasowanie.

---

## CASE

```sql
SELECT
    CASE
        WHEN warunek THEN 'A'
        ELSE 'B'
    END AS wynik;
```

`CASE` pozwala dodać logikę warunkową do wyników zapytania.

---
