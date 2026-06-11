# Skill 03: Research orzecznictwa z realnego źródła (SAOS)

> Skill MateMatic do wgrania do Claude. Wersja DEMO lead magnetu.

## Po co to

Gdy pytasz Claude "jakie jest orzecznictwo do art. X", model potrafi wymyślić sygnatury, które nie istnieją. Lekarstwem nie jest lepszy prompt - jest **realne źródło**. SAOS (System Analizy Orzeczeń Sądowych, Fundacja ePaństwo) to darmowa, publiczna baza orzeczeń SN, TK, KIO i sądów powszechnych z API.

## Workflow

1. **Nie pytaj modelu o sygnatury z pamięci.** Zamiast tego sformułuj zapytanie do SAOS: fraza, przepis, zakres dat, sąd.
2. **Pobierz realne trafienia** z saos.org.pl (wyszukiwarka publiczna) - sygnatura, data, sąd, fragment uzasadnienia.
3. **Pracuj tylko na pobranym tekście.** Każdą tezę, którą przypiszesz orzeczeniu, zweryfikuj wobec pobranego uzasadnienia (patrz Skill 01), nie wobec tego, co model "pamięta".
4. **Oznacz proweniencję.** Przy każdej tezie zapisz, z którego orzeczenia (sygnatura + data) i z którego fragmentu pochodzi.

## Reguła żelazna

Sygnatura, której nie pobrałeś z bazy, nie istnieje, dopóki jej nie znajdziesz. Brak trafienia to wynik, nie porażka - lepiej "nie znalazłem" niż zmyślony II CSK 999/99.

## Format wyniku

Lista: `sygnatura | data | sąd | teza (z pobranego fragmentu) | link/źródło`. Wyraźnie oddziel "potwierdzone w SAOS" od "hipoteza do sprawdzenia".

## Granice

DEMO uczące metody. Pełna wersja (konektor MCP do SAOS + automatyczne pobieranie i grounding, plus EUR-Lex/CJEU i scraping źródeł spoza SAOS, lokalnie) to stack MateMatic/PATRON. SAOS nie zawiera wszystkich orzeczeń; brak w bazie ≠ orzeczenie nie istnieje. Nie zastępuje porady prawnej.

---
© MateMatic · Wiesław Mazur · matematicsolutions.com
