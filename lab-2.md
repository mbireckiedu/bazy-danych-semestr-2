# Ćwiczenie 2 SQL (JOIN, GROUP BY, HAVING)

---

## Uruchomienie środowiska

W ćwiczeniu korzystamy z tej samej bazy danych co w ćwiczeniu nr 1.

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

* uruchomienie Dockera
* start MySQL
* wykonanie skryptów SQL

---

## Punktacja

Do zdobycia: **12 punktów**

* Zadanie 1–5: po **2 pkt**
* Zadanie 6: **BONUS 2 pkt**

Skala ocen:

* 0–4.5 → 2.0
* 5–5.5 → 3.0
* 6–6.5 → 3.5
* 7–8 → 4.0
* 8.5–9 → 4.5
* 9.5– → 5.0

---

# Zadania

---

### Zadanie 1 (2 pkt)

Wyświetl listę zamówień wraz z:

* `ord_id`
* `ord_status`
* imieniem i nazwiskiem użytkownika
* nazwą apteki

---

### Zadanie 2 (2 pkt)

Wyświetl wszystkie pozycje zamówień:

* numer zamówienia
* nazwa leku
* ilość
* cena

---

### Zadanie 3 (2 pkt)

Dla każdego zamówienia policz liczbę pozycji w zamówieniu.

---

### Zadanie 4 (2 pkt)

Policz ile zamówień złożył każdy użytkownik.

Zwróć:

* `usr_id`
* imię i nazwisko
* liczba zamówień

---

### Zadanie 5 (2 pkt)

Policz łączną wartość każdego zamówienia:

```
wartość = ilość * cena
```

---

### Zadanie 6 (BONUS 2 pkt)

Znajdź użytkowników, którzy złożyli więcej niż 1 zamówienie. Wyświetl imię, naziwsko i ilość zamówień.

---

## Zasady oddania

* pliki `.sql` z zapytaniami
* zrzuty ekranu
* dla kazdego zadania proszę stworzyć osobny katalog w repozytorium
* commit plików do repozytorium

---

## Wskazówki

### JOIN

`JOIN służy do łączenia danych z wielu tabel na podstawie powiązanych kolumn.`

```sql
SELECT *
FROM `order` o
JOIN user u ON o.ord_usr_id = u.usr_id
```

---

### GROUP BY

`GROUP BY grupuje wiersze według wskazanej kolumny, aby można było wykonać obliczenia dla każdej grupy.`

```sql
SELECT ori_ord_id, COUNT(*)
FROM order_drug
GROUP BY ori_ord_id
```

---

### SUM

`SUM oblicza łączną wartość dla wskazanego wyrażenia, np. sumę wartości pozycji zamówienia.`

```sql
SELECT SUM(ori_qty * ori_price)
FROM order_drug
```

---

### HAVING

`HAVING filtruje wyniki po grupowaniu, czyli działa na danych już zagregowanych.`

```sql
SELECT ord_usr_id, COUNT(*)
FROM `order`
GROUP BY ord_usr_id
HAVING COUNT(*) > 1
```


---

