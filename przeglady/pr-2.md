# PR #2: web: nowa stopka

**Werdykt:** MERGE

## 3 najważniejsze powody
1. Zmiana dotyczy jednej linii statycznego tekstu w `app/web/html/index.html:64`. Nie rusza JS, CSS, API, Helma ani workflowów.
2. Diff nie zawiera sekretów, obrazów z tagiem latest, `permissions: write-all` ani nieprzypiętych akcji.
3. Opis jasno mówi, co się zmienia i dlaczego (zamówienia składane tuż przed 15:00), oraz podaje, jak sprawdzić zmianę i ją wycofać.

## Blokery
- brak

## Uwagi
- `app/web/html/index.html:64`: separator „·” i półpauza „–” to znaki spoza ASCII. Zgadzają się z dotychczasowym tekstem, więc ryzyko jest pomijalne.
- `build` i `deploy` mają stan skipping. Najpewniej uruchamiają się dopiero po merge na `main`, jak sugeruje opis PR-a. Nie sprawdzałem tego w workflowie.

## Checki
- build: skipping
- deploy: skipping
- test-orders-api: pass
- test-payments: pass
