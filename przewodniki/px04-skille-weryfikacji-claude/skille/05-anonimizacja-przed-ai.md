# Skill 05: Anonimizacja danych przed wrzuceniem do AI

> Skill MateMatic do wgrania do Claude. Wersja DEMO lead magnetu.

## Po co to

Gdy wklejasz fragment sprawy do narzędzia AI w chmurze, treść wychodzi poza kancelarię. Zapytanie prawnika rzadko jest abstrakcyjne - częściej niesie dane, po których da się rozpoznać klienta. To przetwarzanie danych (art. 5 ust. 1 lit. b i art. 28 RODO) i materia tajemnicy zawodowej (art. 6 Prawa o adwokaturze, art. 3 ustawy o radcach prawnych), która nie zna wyjątku "bo pytałem AI". Ten skill każe Ci oczyścić tekst, zanim cokolwiek wyśle.

## Workflow

1. **Wykryj identyfikatory** w tekście: imiona i nazwiska, PESEL, NIP, REGON, numery KRS, adresy, numery spraw/akt, IBAN, daty graniczne, nazwy firm, nietypowe szczegóły pozwalające rozpoznać podmiot.
2. **Zamień na deterministyczne pseudonimy:** Osoba A, Spółka B, [PESEL], [NIP], Miasto C - tak, by tekst zachował sens prawny, ale stracił tożsamość. Trzymaj spójną mapę (Osoba A = ta sama osoba w całym tekście).
3. **Zachowaj mapę lokalnie** (u siebie, nie w prompt do chmury), żeby móc odtworzyć realne dane w finalnym dokumencie.
4. **Zadaj pytanie na oczyszczonym tekście.** Po otrzymaniu odpowiedzi podstaw realne dane z mapy z powrotem - lokalnie.

## Reguła

Pisz każde zapytanie tak, jakby czytał je ktoś z drugiej strony stołu. Jeśli po anonimizacji nadal da się rozpoznać klienta - nie wysyłaj, oczyść głębiej.

## Format wyniku

`Tekst oczyszczony (do wysłania) | Mapa pseudonimów (zostaje u Ciebie) | Lista wykrytych identyfikatorów`.

## Granice

DEMO. Pełna wersja (deterministyczna anonimizacja offline z wykrywaniem polskich PII, oraz - co ważniejsze - architektura, w której akta w ogóle nie muszą wychodzić do chmury) to stack MateMatic/PATRON. Anonimizacja zmniejsza ryzyko, nie usuwa go w całości; przy danych szczególnie wrażliwych rozważ, czy chmura jest w ogóle właściwa. Nie zastępuje porady prawnej ani oceny DPIA.

---
© MateMatic · Wiesław Mazur · matematicsolutions.com
