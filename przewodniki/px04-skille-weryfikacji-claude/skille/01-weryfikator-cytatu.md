# Skill 01: Weryfikator cytatu prawnego (anti-halucynacja)

> Skill MateMatic do wgrania do Claude (projekt / Claude Code). Wersja DEMO lead magnetu.
> Pełna, zautomatyzowana wersja (string-match do bazy SAOS/EUR-Lex, działanie lokalne zero-cloud) jest częścią PATRON. Tu uczysz Claude metody ręcznie.

## Po co to

Model językowy potrafi napisać fragment wyroku, który brzmi idealnie - sygnatura, ton sądu, słownictwo - a którego w orzeczeniu nigdy nie było. Opinia cytująca nieistniejący fragment SN to katastrofa zawodowa i ryzyko odpowiedzialności (art. 6 Prawa o adwokaturze, należyta staranność). Ten skill każe Claude **udowodnić** każdy cytat, zamiast wierzyć mu na słowo.

## Zasada nadrzędna

**Cytat niezweryfikowany = cytat zmyślony, dopóki nie udowodnisz inaczej.** Ciężar dowodu jest odwrócony: to cytat musi się znaleźć w źródle, nie źródło ma obalać cytat.

## Gradient weryfikacji - trzy poziomy

Dla każdego powołania w tekście oznacz, na którym poziomie zostało potwierdzone:

| Poziom | Co potwierdza | Stosuj do |
|---|---|---|
| ISTNIENIE | sygnatura / CELEX, data, organ są realne i zgodne z deklaracją | "wyrok z 12.03.2019, II CSK…", "por. II CSK 123/19" |
| TREŚĆ | źródło co do istoty zawiera to, co twierdzi tekst | "SN przyjął, że…", parafraza holdingu |
| FRAGMENT | cytowany akapit/zdanie istnieje dosłownie w źródle | każdy cytat w cudzysłowie, każdy pinpoint akapitu |

## Workflow (krok po kroku dla Claude)

1. **Wypisz wszystkie powołania** z tekstu: sygnatury, daty, organy, cytaty w cudzysłowie, parafrazy holdingu ("sąd uznał, że…"), powołane przepisy.
2. **Dla każdego ustal wymagany poziom.** Cytat w cudzysłowie wymaga FRAGMENT. Parafraza "SN przyjął" wymaga TREŚĆ. Samo "por. sygnatura" wymaga ISTNIENIE.
3. **Sprawdź wobec źródła** (wklejone orzeczenie / odpis / ustawa). Porównuj znormalizowany tekst: pomiń różnice wielkości liter, spacji, deklinacji, ale NIE zmieniaj słów. Match jest, albo go nie ma.
4. **Złap dwie pułapki:**
   - *Zmyślona sygnatura:* jeśli kotwicy nie da się rozwiązać lub data/organ się nie zgadzają → flaga CZERWONA (możliwe fałszerstwo), nie "luka do uzupełnienia".
   - *Prawdziwy cytat, fałszywa teza:* cytat może być dosłownie obecny (FRAGMENT zielony), a zdanie wokół niego ("SN uznał, że…") przekręca to, co sąd orzekł. Parafraza NIE jest zwolniona z weryfikacji - sprawdzasz ją na poziomie TREŚĆ.
5. **Kalibracja.** Jeśli tekst twierdzi na poziomie FRAGMENT (dosłowny cytat), a weryfikacja dochodzi tylko do TREŚĆ → złagodź do parafrazy albo oznacz pinpoint jako prowizoryczny. Nie podnoś siły twierdzenia ponad osiągnięty poziom.

## Format wyniku

Tabela: `powołanie | wymagany poziom | osiągnięty poziom | status (ZIELONY/KALIBRACJA/CZERWONY) | uwaga`.
Na końcu: lista CZERWONYCH (do usunięcia lub poprawienia PRZED wysłaniem) i jedno zdanie werdyktu.

## Kiedy odpalać

Zawsze przed wysłaniem opinii / memo / pisma procesowego do klienta lub sądu. Zawsze gdy tekst zawiera choć jedną sygnaturę albo cudzysłów z wyroku.

## Granice (uczciwie)

To DEMO uczące dyscypliny. Nie zastępuje porady prawnej. Weryfikacja potwierdza **istnienie i zgodność cytatu ze źródłem**, nie poprawność merytoryczną tezy. Pełna wersja (automatyczny string-match do bazy orzeczeń, działanie offline bez wysyłania akt do chmury) to PATRON - tu robisz to ręcznie, na wklejonym źródle.

---
© MateMatic · Wiesław Mazur · matematicsolutions.com · Skill clean-room, metodyka własna.
