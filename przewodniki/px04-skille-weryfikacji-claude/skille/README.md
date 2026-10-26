# Skille weryfikacji do Claude - paczka PX/04

5 skilli MateMatic do wgrania do Claude. Wersja demonstracyjna - uczy metody, pełna automatyzacja jest w produktach MateMatic.

Przewodnik: https://matematicsolutions.com/akademia/px04-skille-weryfikacji-claude

## Pozycjonowanie

**Inni dają Ci wiedzę na wejściu. My sprawdzamy wynik na wyjściu.**

Pakiety wiedzy i prompt-packi robią jedno: zasilają Claude kontekstem na starcie - przepisami, orzecznictwem, wzorami - i ufają, że dalej sprawdzisz wynik sam. To pomaga modelowi pisać. Nie sprawdza, czy to, co napisał, jest prawdziwe.

Ta paczka to **druga warstwa**: weryfikacja wyjścia. Każdy skill ma jeden mechanizm - sprawdza, czy sygnatura istnieje, czy cytat jest w wyroku, czy dane klienta nie wyciekły. Działa na tym, czego już używasz, także na wyniku z cudzego pakietu wiedzy.

## Co jest w środku

Każdy skill to folder z plikiem `SKILL.md` (nagłówek z polami `name` i `description`).

1. `weryfikator-cytatu` - gradient ISTNIENIE / TREŚĆ / FRAGMENT; każe Claude udowodnić każdą sygnaturę i cytat, zamiast wierzyć mu na słowo. Flagowy.
2. `triage-zadania` - najpierw klasyfikacja (stawka, złożoność), potem dobór narzędzi; chroni przed paleniem czasu na rutynie i przepuszczeniem sprawy wysokiej stawki.
3. `research-orzecznictwa-saos` - realne źródło zamiast sygnatur z pamięci modelu.
4. `red-team-pisma` - zaatakuj własną tezę, zanim zrobi to przeciwnik albo sąd.
5. `anonimizacja-przed-ai` - zastąp dane identyfikujące pseudonimami, zanim cokolwiek wyślesz do chmury. To pseudonimizacja, nie anonimizacja: mapa zostaje u Ciebie, a tekst nadal podlega RODO i tajemnicy zawodowej.

## Jak użyć

- **Projekt w Claude.ai** - wklej treść `SKILL.md` do instrukcji projektu (Project instructions).
- **Skill w Claude.ai** - wgraj folder skilla spakowany do ZIP, każdy skill osobno. Dostępność skilli zależy od planu i włączonego wykonywania kodu: https://support.claude.com/en/articles/12512180-using-skills-in-claude
- **Claude Code** - skopiuj foldery skilli do `~/.claude/skills/`.

## Czego ta paczka nie robi

- To demo metody, nie produkt produkcyjny. Weryfikacja jest tu ręczna (na wklejonym źródle); automatyczne porównanie z bazą orzeczeń, działanie offline i pełne pokrycie (KIO, UODO, KRS, EUR-Lex) to PATRON i usługi MateMatic.
- Żaden skill nie zastępuje porady prawnej ani osądu prowadzącego sprawę.
- Weryfikacja potwierdza istnienie i zgodność cytatu ze źródłem, nie poprawność merytoryczną tezy.

## Licencja i pochodzenie

Treść na licencji Creative Commons Uznanie autorstwa - Na tych samych warunkach 4.0 (CC BY-SA 4.0): możesz używać, kopiować i rozwijać, z uznaniem autorstwa MateMatic i na tej samej licencji. Metodyka i treść własne MateMatic (clean-room). Inspiracja gradientu weryfikacji: jeannesulzer/international-criminal-tribunals-skills (CC BY 4.0) - kod i prompty od zera.

Źródło: https://github.com/matematicsolutions/praxis

---
© 2026 MateMatic · Wiesław Mazur · matematicsolutions.com
