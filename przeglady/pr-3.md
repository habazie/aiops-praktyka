# PR #3: orders-api: szybciej

**Werdykt:** NIE MERGUJ

## 3 najważniejsze powody
1. Obraz `orders-api` dostaje tag `latest` (`app/deploy/helm/kantyna/values.yaml:78`). Wdrożenie przestaje być powtarzalne, a przy `pullPolicy: IfNotPresent` węzły mogą uruchamiać różne wersje.
2. Usunięte `resources.limits` dla `orders-api` (po `app/deploy/helm/kantyna/values.yaml:92`). Kantyna ma przełączniki `memory_leak_mb_per_min` i `cpu_burn`, więc pod bez limitów może zabrać zasoby całemu węzłowi na współdzielonym klastrze.
3. Opis „drobne poprawki” nie mówi, co i dlaczego się zmienia. Tytuł „szybciej” nie ma pokrycia w diffie: żadna zmiana nie przyspiesza aplikacji.

## Blokery
- `app/deploy/helm/kantyna/values.yaml:78` — obraz z tagiem latest: `ordersApi.image.tag: latest`

## Uwagi
- `app/deploy/helm/kantyna/values.yaml:92` — usunięte `resources.limits` (`cpu: 500m`, `memory: 384Mi`). Reguła POPRAW z REVIEW.md. `requests` zostały.
- Opis PR-a — „drobne poprawki” nie spełnia reguły „opis mówi, co i dlaczego się zmienia” (POPRAW).
- Pipeline nadpisuje tag przez `--set global.imageTag`. Czy przykrywa to `ordersApi.image.tag`, zależy od helpera `kantyna.image`. Ta komenda nie widzi tego pliku, więc nie sprawdziłem. `latest` w values blokuje merge niezależnie od tego.

## Checki
- test-orders-api — pass
- test-payments — pass
- build — skipping (PR, nie push na main)
- deploy — skipping (PR, nie push na main)
