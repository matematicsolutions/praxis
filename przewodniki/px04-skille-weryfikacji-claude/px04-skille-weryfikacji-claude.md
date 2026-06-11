# PX/04 - Skille weryfikacji do Claude dla kancelarii

> Praxis - przewodniki praktyczne MateMatic. Podtyp: podrecznik proceduralny (skille).
> Wersja v1.0. Wersja webowa: https://matematicsolutions.com/akademia/px04-skille-weryfikacji-claude.html
> Licencja: CC BY-SA 4.0. Uwagi i poprawki: GitHub Issues / Pull Requests.
> Otwarty kod pieciu skilli: katalog ./skille/ w tym repozytorium.

**Eyebrow:** Akademia · Praxis · Skille · v1.0
**Kod:** PX/04
**Status MateMatic:** otwarte
**Format:** 5 skilli .md do wgrania do Claude

## H1

Skille weryfikacji do Claude. Piec skilli, ktore sprawdzaja, co AI napisalo.

## Lede

Pakiety wiedzy i prompt-packi robia jedno: zasilaja Claude kontekstem na starcie i ufaja, ze dalej sprawdzisz wynik sam. To pomaga modelowi pisac. Nie sprawdza, czy to, co napisal, jest prawdziwe. Ten przewodnik to druga warstwa: piec skilli do wgrania do Claude, ktore weryfikuja wyjscie - czy sygnatura istnieje, czy cytat jest w wyroku, czy dane klienta nie wyciekly. Dzialaja na tym, czego juz uzywasz.

## Hook

Model potrafi napisac fragment wyroku, ktorego w orzeczeniu nigdy nie bylo - sygnatura, ton sadu, slownictwo sie zgadzaja. Pytanie nie brzmi, czy Claude pisze ladnie. Brzmi: czy sprawdziles, zanim wyslales.

---

## Scope box

**Dla kogo:** radcy i adwokaci pracujacy z Claude, prawnicy in-house, compliance officerowie, aplikanci, kazdy, kto wkleja sprawe do AI i odpowiada za wynik.

**Czego ten przewodnik NIE obejmuje:** pelnej, zautomatyzowanej weryfikacji (string-match do bazy orzeczen, dzialanie offline, pelne resolvery KIO/UODO/KRS i EUR-Lex) - to stack MateMatic i PATRON; tu uczysz metody recznie, na wklejonym zrodle. Nie jest to tez pakiet wiedzy merytorycznej - skille sprawdzaja wynik, nie zastepuja znajomosci prawa.

**Zastrzezenie:** skille sa narzedziem kontroli, nie zastepuja porady prawnej ani osadu prowadzacego sprawe. Weryfikacja potwierdza istnienie i zgodnosc cytatu ze zrodlem, nie poprawnosc merytoryczna tezy. Wszystkie odniesienia do RODO, AI Act i tajemnicy zawodowej to interpretacja MateMatic, nie stanowisko PUODO, NRA ani KRRP.

---

## Modul 0 - Dlaczego weryfikacja wyjscia

### Problem

Rynek narzedzi AI dla prawnikow rozwiazuje jeden problem: jak dac modelowi dobra wiedze na wejsciu. Pakiety wiedzy, biblioteki promptow, projekty z wgranym orzecznictwem - wszystko po to, zeby Claude pisal madrzej. To wartosciowe. Ale zostawia druga polowe pusta: nikt nie sprawdza, czy to, co model wygenerowal, jest prawdziwe. Weryfikacje wyjscia ciszej przerzuca sie na prawnika, ktory "przeciez sprawdzi".

### Dwie warstwy, nie jedna

Kontekst na wejsciu i weryfikacja na wyjsciu to dwie rozne rzeczy. Dobry pakiet wiedzy zmniejsza szanse, ze Claude zmysli - nie usuwa jej. Model nadal potrafi wyprodukowac sygnature, ktorej nie ma, albo przypisac sadowi teze, ktorej ten nie postawil. Piec skilli z tego przewodnika to druga warstwa: kontrola tego, co juz powstalo. Dzialaja niezaleznie od tego, jakiego pakietu wiedzy uzywasz - takze na cudzym.

### Zasada nadrzedna

**Cytat niezweryfikowany = cytat zmyslony, dopoki nie udowodnisz inaczej.** Ciezar dowodu jest odwrocony: to cytat musi sie znalezc w zrodle, nie zrodlo ma obalac cytat.

### Kontekst prawny w skrocie

Pismo cytujace nieistniejacy fragment wyroku to nie wpadka stylistyczna, to ryzyko zawodowe (art. 6 Prawa o adwokaturze, art. 3 ustawy o radcach prawnych, nalezyta starannosc). Glosne sprawy w USA - od Mata v. Avianca (S.D.N.Y. 2023), gdzie sad ukaral pelnomocnikow za powolanie nieistniejacych, zmyslonych przez ChatGPT wyrokow - pokazaly, czym to sie konczy. Polski prawnik ma ten sam obowiazek sprawdzenia.

*Interpretacja MateMatic, nie stanowisko PUODO, NRA ani KRRP.*

---

## Modul 1 - Weryfikator cytatu

Gradient weryfikacji - trzy poziomy: **ISTNIENIE** (sygnatura, data, organ realne i zgodne), **TRESC** (zrodlo co do istoty zawiera twierdzenie, dotyczy parafraz "sad przyjal, ze..."), **FRAGMENT** (cytowany akapit istnieje doslownie).

Procedura: (1) wypisz wszystkie powolania; (2) ustal wymagany poziom (cudzyslow -> FRAGMENT, parafraza -> TRESC, "por. sygnatura" -> ISTNIENIE); (3) sprawdz wobec zrodla string-matchem znormalizowanego tekstu - match jest albo go nie ma; (4) pulapka zmyslonej sygnatury: nierozwiazana kotwica = flaga czerwona, nie luka; (5) pulapka prawdziwy-cytat-falszywa-teza: parafraze sprawdz na poziomie TRESC; (6) kalibracja: nie podnos sily twierdzenia ponad osiagniety poziom.

Pelny skill: [skille/01-weryfikator-cytatu.md](skille/01-weryfikator-cytatu.md).

---

## Modul 2 - Triage zadania

Najpierw sklasyfikuj zadanie (stawka, zlozonosc), potem dobierz narzedzia. Sciezki: rutyna -> zwykla odpowiedz; cytaty -> Weryfikator cytatu (Skill 01); high-stakes -> red-team (Skill 04) + weryfikacja; dane wrazliwe -> najpierw anonimizacja (Skill 05). Sprawdz wejscie: cel, podmiot, fakty, ograniczenia; brak -> pytania do klienta przed startem.

Pelny skill: [skille/02-triage-zadania.md](skille/02-triage-zadania.md).

---

## Modul 3 - Research orzecznictwa z SAOS

Lekarstwem na zmyslone sygnatury nie jest lepszy prompt, tylko realne zrodlo. SAOS (System Analizy Orzeczen Sadowych, Fundacja ePanstwo) to darmowa baza orzeczen SN, TK, KIO i sadow powszechnych z API. Nie pytaj modelu o sygnatury z pamieci - pobierz realne trafienia, pracuj na pobranym tekscie, oznacz proweniencje. Sygnatura, ktorej nie pobrales z bazy, nie istnieje, dopoki jej nie znajdziesz.

Pelny skill: [skille/03-research-orzecznictwa-saos.md](skille/03-research-orzecznictwa-saos.md).

---

## Modul 4 - Red-team pisma

Zaatakuj wlasna teze, zanim zrobi to przeciwnik albo sad. Cztery role po kolei: **builder** (najmocniejsza wersja tezy), **attacker** (atak bez litosci - kontrargumenty, kontr-orzecznictwo, luki), **synthesizer** (ktore ataki wymagaja zmiany pisma), **verifier** (czy teza sie trzyma, czy kontr-orzecznictwo prawdziwe). Tylko dla spraw wysokiej stawki - triage podpowie, czy warto.

Pelny skill: [skille/04-red-team-pisma.md](skille/04-red-team-pisma.md).

---

## Modul 5 - Anonimizacja przed AI

Wklejajac sprawe do AI w chmurze, tresc wychodzi poza kancelarie. To przetwarzanie w innym celu niz powierzono (art. 5 ust. 1 lit. b i art. 28 RODO) i materia tajemnicy zawodowej (art. 6 PoA, art. 3 ustawy o radcach), ktora nie zna wyjatku "bo pytalem AI". Wykryj identyfikatory (imiona, PESEL, NIP, REGON, KRS, adresy, numery akt, IBAN, nazwy firm), zamien na deterministyczne pseudonimy, mape trzymaj lokalnie, pytaj na oczyszczonym tekscie.

*Interpretacja MateMatic, nie stanowisko PUODO, NRA ani KRRP.*

Pelny skill: [skille/05-anonimizacja-przed-ai.md](skille/05-anonimizacja-przed-ai.md).

---

## Modul 6 - Zlozenie: jak wgrac i uzywac

Kazdy skill to plik tekstowy. Wgrywasz raz, uzywasz w nieskonczonosc. Dwie sciezki: **Claude.ai** (wklej tresc skilla do instrukcji projektu) albo **Claude Code** (plik jako skill w katalogu skilli).

Kolejnosc: (1) Triage (S02) - czy zadanie wymaga ciezszej weryfikacji; (2) Anonimizacja (S05) - jesli wejscie niesie dane klienta; (3) Research z SAOS (S03) - do orzecznictwa; (4) Weryfikator cytatu (S01) - przed wyslaniem kazdego pisma z cytatami, bramka nienegocjowalna; (5) Red-team (S04) - dla spraw wysokiej stawki, na koniec.

---

## Zrodla i pochodzenie

- SAOS - System Analizy Orzeczen Sadowych, Fundacja ePanstwo (https://saos.org.pl).
- Metodyka i tresc skilli - wlasne MateMatic (clean-room). Inspiracja gradientu weryfikacji ISTNIENIE/TRESC/FRAGMENT: jeannesulzer/international-criminal-tribunals-skills (CC BY 4.0); kod i prompty napisane od zera.
- Pelny stack weryfikacji (citation-grounding, osobne weryfikatory KIO/UODO/KRS, pakiet audytowy AI Act art. 12) jest czescia PATRON.

Skille sa narzedziem kontroli wyniku AI, nie zastepuja porady prawnej. Weryfikacja potwierdza istnienie i zgodnosc cytatu ze zrodlem, nie poprawnosc merytoryczna tezy.

---

## Changelog

- v1.0 (2026-06-11) - pierwsza publikacja. 7 modulow, 5 skilli do pobrania (katalog ./skille/).
