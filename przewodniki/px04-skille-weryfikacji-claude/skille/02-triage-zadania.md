# Skill 02: Triage zadania prawnego (która ścieżka, ile kontroli)

> Skill MateMatic do wgrania do Claude. Wersja DEMO lead magnetu.

## Po co to

Nie każde zapytanie zasługuje na ten sam wysiłek. Rutynowe pytanie marnuje czas, gdy traktujesz je jak sprawę życia. Sprawa wysokiej stawki przepuszczona bez kontroli to ryzyko. Ten skill każe Claude **najpierw sklasyfikować** zadanie, a dopiero potem dobrać narzędzia.

## Workflow

1. **Oceń stawkę.** Kto jest adresatem outputu (notatka wewnętrzna / klient / sąd / organ)? Co się stanie, jeśli będzie błędny (zażenowanie / strata pieniędzy / odpowiedzialność zawodowa)?
2. **Oceń złożoność.** Czy odpowiedź wymaga orzecznictwa? Interpretacji spornej? Wielu reżimów (RODO + KK + umowa)? Czy fakty są kompletne?
3. **Przypisz ścieżkę:**
   - *Rutyna* (niska stawka, niska złożoność) → zwykła odpowiedź, bez ciężkiej weryfikacji.
   - *Cytaty* (output powołuje orzeczenia/przepisy) → uruchom Weryfikator cytatu (Skill 01) przed wysłaniem.
   - *High-stakes* (opinia, memo DD, pismo procesowe) → kontradyktoryjny red-team (Skill 04) + weryfikacja cytatu + kontrola wierności.
   - *Dane wrażliwe na wejściu* → najpierw anonimizacja (Skill 05).
4. **Sprawdź wejście.** Czy masz dość, by zacząć - jasny cel, podmiot, fakty, ograniczenia? Jeśli nie, wypisz luki i pytania do klienta ZANIM ruszysz (nie zgaduj).

## Format wyniku

`stawka: niska/średnia/wysoka | złożoność: niska/średnia/wysoka | ścieżka: … | brakujące informacje: … | uzasadnienie: jedno zdanie`.

## Granice

DEMO. Pełna wersja (router automatycznie spinający weryfikatory i pakiet audytowy AI Act) to PATRON. Nie zastępuje porady prawnej.

---
© MateMatic · Wiesław Mazur · matematicsolutions.com
