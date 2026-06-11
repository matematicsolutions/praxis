# PX/04 - Skille weryfikacji do Claude dla kancelarii

> Praxis - przewodniki praktyczne MateMatic. Podtyp: podręcznik proceduralny (skille).
> Wersja v1.0. Wersja webowa: https://matematicsolutions.com/akademia/px04-skille-weryfikacji-claude.html
> Licencja: CC BY-SA 4.0. Uwagi i poprawki: GitHub Issues / Pull Requests.
> Otwarty kod pięciu skilli: katalog ./skille/ w tym repozytorium.

**Eyebrow:** Akademia · Praxis · Skille · v1.0
**Kod:** PX/04
**Status MateMatic:** otwarte
**Format:** 5 skilli .md do wgrania do Claude

## H1

Skille weryfikacji do Claude. Pięć skilli, które sprawdzają, co AI napisało.

## Lede

Pakiety wiedzy i prompt-packi robią jedno: zasilają Claude kontekstem na starcie i ufają, że dalej sprawdzisz wynik sam. To pomaga modelowi pisać. Nie sprawdza, czy to, co napisał, jest prawdziwe. Ten przewodnik to druga warstwa: pięć skilli do wgrania do Claude, które weryfikują wyjście - czy sygnatura istnieje, czy cytat jest w wyroku, czy dane klienta nie wyciekły. Działają na tym, czego już używasz.

## Hook

Model potrafi napisać fragment wyroku, którego w orzeczeniu nigdy nie było - sygnatura, ton sądu, słownictwo się zgadzają. Pytanie nie brzmi, czy Claude pisze ładnie. Brzmi: czy sprawdziłeś, zanim wysłałeś.

---

## Scope box

**Dla kogo:** radcy i adwokaci pracujący z Claude, prawnicy in-house, compliance officerowie, aplikanci, każdy, kto wkleja sprawę do AI i odpowiada za wynik.

**Czego ten przewodnik NIE obejmuje:** pełnej, zautomatyzowanej weryfikacji (string-match do bazy orzeczeń, działanie offline, pełne resolvery KIO/UODO/KRS i EUR-Lex) - to stack MateMatic i PATRON; tu uczysz metody ręcznie, na wklejonym źródle. Nie jest to też pakiet wiedzy merytorycznej - skille sprawdzają wynik, nie zastępują znajomości prawa.

**Zastrzeżenie:** skille są narzędziem kontroli, nie zastępują porady prawnej ani osądu prowadzącego sprawę. Weryfikacja potwierdza istnienie i zgodność cytatu ze źródłem, nie poprawność merytoryczną tezy. Wszystkie odniesienia do RODO, AI Act i tajemnicy zawodowej to interpretacja MateMatic, nie stanowisko PUODO, NRA ani KRRP.

---

## Moduł 0 - Dlaczego weryfikacja wyjścia

### Problem

Rynek narzędzi AI dla prawników rozwiązuje jeden problem: jak dać modelowi dobrą wiedzę na wejściu. Pakiety wiedzy, biblioteki promptów, projekty z wgranym orzecznictwem - wszystko po to, żeby Claude pisał mądrzej. To wartościowe. Ale zostawia drugą połowę pustą: nikt nie sprawdza, czy to, co model wygenerował, jest prawdziwe. Weryfikację wyjścia ciszej przerzuca się na prawnika, który "przecież sprawdzi".

### Dwie warstwy, nie jedna

Kontekst na wejściu i weryfikacja na wyjściu to dwie różne rzeczy. Dobry pakiet wiedzy zmniejsza szansę, że Claude zmyśli - nie usuwa jej. Model nadal potrafi wyprodukować sygnaturę, której nie ma, albo przypisać sądowi tezę, której ten nie postawił. Pięć skilli z tego przewodnika to druga warstwa: kontrola tego, co już powstało. Działają niezależnie od tego, jakiego pakietu wiedzy używasz - także na cudzym.

### Zasada nadrzędna

**Cytat niezweryfikowany = cytat zmyślony, dopóki nie udowodnisz inaczej.** Ciężar dowodu jest odwrócony: to cytat musi się znaleźć w źródle, nie źródło ma obalać cytat.

### Kontekst prawny w skrócie

Pismo cytujące nieistniejący fragment wyroku to nie wpadka stylistyczna, to ryzyko zawodowe (art. 6 Prawa o adwokaturze, art. 3 ustawy o radcach prawnych, należyta staranność). Głośne sprawy w USA - od Mata v. Avianca (S.D.N.Y. 2023), gdzie sąd ukarał pełnomocników za powołanie nieistniejących, zmyślonych przez ChatGPT wyroków - pokazały, czym to się kończy. Polski prawnik ma ten sam obowiązek sprawdzenia.

*Interpretacja MateMatic, nie stanowisko PUODO, NRA ani KRRP.*

---

## Moduł 1 - Weryfikator cytatu

Gradient weryfikacji - trzy poziomy: **ISTNIENIE** (sygnatura, data, organ realne i zgodne), **TREŚĆ** (źródło co do istoty zawiera twierdzenie, dotyczy parafraz "sąd przyjął, że..."), **FRAGMENT** (cytowany akapit istnieje dosłownie).

Procedura: (1) wypisz wszystkie powołania; (2) ustal wymagany poziom (cudzysłów -> FRAGMENT, parafraza -> TREŚĆ, "por. sygnatura" -> ISTNIENIE); (3) sprawdź wobec źródła string-matchem znormalizowanego tekstu - match jest albo go nie ma; (4) pułapka zmyślonej sygnatury: nierozwiązana kotwica = flaga czerwona, nie luka; (5) pułapka prawdziwy-cytat-fałszywa-teza: parafrazę sprawdź na poziomie TREŚĆ; (6) kalibracja: nie podnoś siły twierdzenia ponad osiągnięty poziom.

Pełny skill: [skille/01-weryfikator-cytatu.md](skille/01-weryfikator-cytatu.md).

---

## Moduł 2 - Triage zadania

Najpierw sklasyfikuj zadanie (stawka, złożoność), potem dobierz narzędzia. Ścieżki: rutyna -> zwykła odpowiedź; cytaty -> Weryfikator cytatu (Skill 01); high-stakes -> red-team (Skill 04) + weryfikacja; dane wrażliwe -> najpierw anonimizacja (Skill 05). Sprawdź wejście: cel, podmiot, fakty, ograniczenia; brak -> pytania do klienta przed startem.

Pełny skill: [skille/02-triage-zadania.md](skille/02-triage-zadania.md).

---

## Moduł 3 - Research orzecznictwa z SAOS

Lekarstwem na zmyślone sygnatury nie jest lepszy prompt, tylko realne źródło. SAOS (System Analizy Orzeczeń Sądowych, Fundacja ePaństwo) to darmowa baza orzeczeń SN, TK, KIO i sądów powszechnych z API. Nie pytaj modelu o sygnatury z pamięci - pobierz realne trafienia, pracuj na pobranym tekście, oznacz proweniencję. Sygnatura, której nie pobrałeś z bazy, nie istnieje, dopóki jej nie znajdziesz.

Pełny skill: [skille/03-research-orzecznictwa-saos.md](skille/03-research-orzecznictwa-saos.md).

---

## Moduł 4 - Red-team pisma

Zaatakuj własną tezę, zanim zrobi to przeciwnik albo sąd. Cztery role po kolei: **builder** (najmocniejsza wersja tezy), **attacker** (atak bez litości - kontrargumenty, kontr-orzecznictwo, luki), **synthesizer** (które ataki wymagają zmiany pisma), **verifier** (czy teza się trzyma, czy kontr-orzecznictwo prawdziwe). Tylko dla spraw wysokiej stawki - triage podpowie, czy warto.

Pełny skill: [skille/04-red-team-pisma.md](skille/04-red-team-pisma.md).

---

## Moduł 5 - Anonimizacja przed AI

Wklejając sprawę do AI w chmurze, treść wychodzi poza kancelarię. To przetwarzanie w innym celu niż powierzono (art. 5 ust. 1 lit. b i art. 28 RODO) i materia tajemnicy zawodowej (art. 6 Prawa o adwokaturze, art. 3 ustawy o radcach prawnych), która nie zna wyjątku "bo pytałem AI". Wykryj identyfikatory (imiona, PESEL, NIP, REGON, KRS, adresy, numery akt, IBAN, nazwy firm), zamień na deterministyczne pseudonimy, mapę trzymaj lokalnie, pytaj na oczyszczonym tekście.

*Interpretacja MateMatic, nie stanowisko PUODO, NRA ani KRRP.*

Pełny skill: [skille/05-anonimizacja-przed-ai.md](skille/05-anonimizacja-przed-ai.md).

---

## Moduł 6 - Złożenie: jak wgrać i używać

Każdy skill to plik tekstowy. Wgrywasz raz, używasz w nieskończoność. Dwie ścieżki: **Claude.ai** (wklej treść skilla do instrukcji projektu) albo **Claude Code** (plik jako skill w katalogu skilli).

Kolejność: (1) Triage (S02) - czy zadanie wymaga cięższej weryfikacji; (2) Anonimizacja (S05) - jeśli wejście niesie dane klienta; (3) Research z SAOS (S03) - do orzecznictwa; (4) Weryfikator cytatu (S01) - przed wysłaniem każdego pisma z cytatami, bramka nienegocjowalna; (5) Red-team (S04) - dla spraw wysokiej stawki, na koniec.

---

## Źródła i pochodzenie

- SAOS - System Analizy Orzeczeń Sądowych, Fundacja ePaństwo (https://saos.org.pl).
- Metodyka i treść skilli - własne MateMatic (clean-room). Inspiracja gradientu weryfikacji ISTNIENIE/TREŚĆ/FRAGMENT: jeannesulzer/international-criminal-tribunals-skills (CC BY 4.0); kod i prompty napisane od zera.
- Pełny stack weryfikacji (citation-grounding, osobne weryfikatory KIO/UODO/KRS, pakiet audytowy AI Act art. 12) jest częścią PATRON.

Skille są narzędziem kontroli wyniku AI, nie zastępują porady prawnej. Weryfikacja potwierdza istnienie i zgodność cytatu ze źródłem, nie poprawność merytoryczną tezy.

---

## Changelog

- v1.0 (2026-06-11) - pierwsza publikacja. 7 modułów, 5 skilli do pobrania (katalog ./skille/).
