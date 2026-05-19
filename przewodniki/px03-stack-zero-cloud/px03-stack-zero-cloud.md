# PX/03 - Stack zero-cloud dla kancelarii

> Praxis - przewodniki praktyczne MateMatic. Podtyp: podrecznik proceduralny.
> Wersja v1.0. Wersja webowa: https://matematicsolutions.com/akademia/px03-stack-zero-cloud.html
> Licencja: CC BY-SA 4.0. Uwagi i poprawki: GitHub Issues / Pull Requests.

**Eyebrow:** Akademia · Praxis · Podrecznik · v1.0
**Kod:** PX/03
**Status MateMatic:** otwarte
**Szacowany czas wdrozenia:** Stack Lite 1-2 tygodnie, Standard 3-5 tygodni

## H1

Stack zero-cloud dla kancelarii. Sześć narzędzi, zero danych w chmurze.

## Lede

Każde popularne narzędzie AI dla prawników - transkrypcja, podpis, notatki - wysyła dane na serwery w USA. Dla kancelarii to nie wygoda, to problem z tajemnicą zawodową i RODO. Ten podręcznik pokazuje, jak złożyć kompletny zestaw sześciu narzędzi open source, które robią to samo, a dane nie opuszczają serwera kancelarii. Krok po kroku, z checklistami do pobrania. Nie teoria - procedura.

## Hook

Jeśli Twój asystent AI działa w przeglądarce i nie wiesz, gdzie trafia nagranie rozmowy z klientem - już masz odpowiedź.

---

## Scope box

**Dla kogo:** wspólnicy i partnerzy kancelarii, compliance officerowie, radcy prowadzący praktykę solo, administratorzy IT kancelarii.

**Czego ten podręcznik NIE obejmuje:** konfiguracji konkretnego serwera (sprzęt kupuje kancelaria), audytu prawnego pod konkretną sprawę, certyfikacji eIDAS QES (to osobny proces z dostawcą), pełnego wdrożenia produkcyjnego z odpowiedzialnością - to robi MateMatic razem z kancelarią.

**Zastrzeżenie:** wszystkie odniesienia do RODO, AI Act i tajemnicy zawodowej w tym podręczniku to interpretacja MateMatic, nie stanowisko NRA ani KRRP. Decyzję o zgodności konkretnego wdrożenia podejmuje kancelaria.

---

## Moduł 0 - Dlaczego zero-cloud

### Problem

Kancelaria używa Otter.ai do transkrypcji przesłuchań, DocuSign do pełnomocnictw, Notion do notatek z akt. Wygodne. Każde z tych narzędzi to usługa działająca na serwerach w USA. Nagranie rozmowy z klientem, treść pełnomocnictwa, notatka o strategii procesowej - wszystko to wychodzi poza kancelarię, zanim ktokolwiek się zastanowił, czy powinno.

### Kontekst prawny w skrócie

Tajemnica zawodowa (art. 6 Prawa o adwokaturze, art. 3 ustawy o radcach prawnych) nie zna wyjątku „bo narzędzie było wygodne". RODO art. 32 wymaga środków technicznych i organizacyjnych adekwatnych do ryzyka - a ryzyko dla akt klienta jest wysokie. Transfer danych do USA wymaga podstawy (DPF, standardowe klauzule umowne), a domyślnie żadne darmowe konto SaaS jej nie zapewnia.

To nie znaczy, że AI jest zakazane. To znaczy: AI tak, ale na warunkach kancelarii, nie dostawcy.

*Interpretacja MateMatic, nie stanowisko NRA ani KRRP.*

### Trzy zasady stacku

1. **Dane nie wychodzą poza serwer kancelarii.** Self-host jest domyślny. Mała kancelaria może powierzyć hosting zaufanemu partnerowi - ale nie globalnej platformie SaaS.
2. **AI lokalne, albo BYOK z umową.** Domyślnie model działa lokalnie (Ollama, Llama, Mistral). Jeśli kancelaria chce użyć Anthropic czy OpenAI - tylko z podpisaną umową powierzenia i wyłączeniem treningu na danych.
3. **Kod otwarty i audytowalny.** Każde narzędzie w stacku to open source. Kancelaria może zlecić audyt bezpieczeństwa - czego przy zamkniętym SaaS zrobić nie może.

### Czego NIE wkładamy do stacku

- **Otter.ai, Fireflies, Tactiq** - transkrypcja w chmurze US, dane wychodzą.
- **DocuSign, Adobe Sign** - podpis w chmurze US, drogo, dane wychodzą.
- **Notion** - brak realnego self-hostu dla małej kancelarii.
- **Chmurowy model AI bez umowy powierzenia** - domyślnie blokada w polityce kancelarii.

### Artefakt do pobrania

**Tabela ryzyka: SaaS vs self-host** - zestawienie sześciu funkcji (transkrypcja, podpis, OCR, notatki, backup, asystent AI) z kolumnami: gdzie trafiają dane, podstawa transferu, kto może zlecić audyt, koszt roczny. Jednostronicowa, do rozmowy z zarządem kancelarii.

### Granica DIY / MateMatic

Zrozumienie zasad i przejście tabeli ryzyka zrobisz sam w godzinę. Mapowanie konkretnego ryzyka na konkretną kancelarię i decyzję, które warstwy wdrożyć w pierwszej kolejności - to audyt, który MateMatic robi z kancelarią.

---

## Moduł 1 - Backup Workspace (gogcli)

### Problem

Kancelaria trzyma akta, korespondencję i kalendarz w Google Workspace. Jedna pomyłka administratora, jeden spór z dostawcą, jeden atak na konto - i ciągłość pracy kancelarii stoi pod znakiem zapytania. RODO art. 32 wymienia „zdolność do szybkiego przywrócenia dostępności danych" wprost.

### Kontekst prawny w skrócie

Art. 32 RODO mówi o ciągłości i odtwarzalności danych jako środku technicznym. Backup poza kontrolą jednego dostawcy to nie nadgorliwość - to realizacja tego obowiązku.

*Interpretacja MateMatic, nie stanowisko NRA ani KRRP.*

### Procedura krok po kroku

1. Zainstaluj gogcli (narzędzie wiersza poleceń do eksportu Google Workspace).
2. Utwórz prywatne repozytorium Git - poza infrastrukturą Google.
3. Wygeneruj klucz szyfrowania (age) i zabezpiecz go offline.
4. Skonfiguruj eksport: poczta, Dysk, Kalendarz, Kontakty.
5. Ustaw harmonogram backupu (np. codziennie w nocy).
6. Zaszyfruj backup kluczem age przed wypchnięciem do repozytorium.
7. Ustal politykę retencji (dla akt kancelarii zwykle 5-10 lat).
8. Przetestuj odtworzenie - backup, którego nie próbowałeś przywrócić, nie istnieje.

### Artefakt do pobrania

**Checklista wdrożenia backupu** - osiem kroków powyżej w formie odhaczalnej, plus pola: lokalizacja klucza age, harmonogram, retencja, data ostatniego testu odtworzenia.

### Pułapki

- Klucz age trzymany w tym samym repozytorium co backup - to jak zostawić klucz w zamku.
- Brak testu odtworzenia - najczęstszy błąd; backup „działa" do dnia, w którym jest potrzebny.
- Retencja krótsza niż okres przechowywania akt.

### Granica DIY / MateMatic

Solo radca z podstawami technicznymi wdroży to sam w pół dnia. Dla kancelarii z zespołem - zarządzanie kluczami, polityka retencji i instrukcja techniczna dla administratora to część wdrożenia z MateMatic.

---

## Moduł 2 - OCR skanów akt (Chandra OCR)

### Problem

Połowa akt w kancelarii to skany - kserówki z sądu, umowy, pisma na papierze bez warstwy tekstowej. Nie da się ich przeszukać, zacytować, podać AI do analizy. Komercyjne OCR online oznacza wysłanie akt klienta na cudzy serwer.

### Kontekst prawny w skrócie

Skan akt to dane osobowe i często dane wrażliwe (art. 9 RODO - sprawy zdrowotne, wyroki). OCR lokalny utrzymuje przetwarzanie w granicach kancelarii.

*Interpretacja MateMatic, nie stanowisko NRA ani KRRP.*

### Procedura krok po kroku

1. Zainstaluj Chandra OCR (inferencja lokalna).
2. Przygotuj pięć reprezentatywnych skanów kancelarii - różna jakość, różne typy pism.
3. Uruchom OCR na próbce testowej.
4. Oceń jakość rozpoznania tekstu polskiego (Chandra w teście MateMatic - 85,3% na polskim).
5. Ustal próg akceptacji - dla jakich dokumentów wynik wystarcza, a które wymagają korekty ręcznej.
6. Wprowadź obieg: skan -> OCR -> weryfikacja -> zapis w aktach.

### Artefakt do pobrania

**Checklista OCR + arkusz testu pięciu skanów** - tabela do wpisania wyniku rozpoznania per dokument i decyzji „akceptuj / koryguj ręcznie".

### Pułapki

- Traktowanie wyniku OCR jako pewnego - przy 85 procentach co siódme słowo może wymagać oka. Dla cytatu do pisma procesowego weryfikacja jest obowiązkowa.
- Skany bardzo niskiej jakości - czasem szybciej przepisać niż poprawiać.

### Granica DIY / MateMatic

Instalacja i test próbki - samodzielnie. Wpięcie OCR w obieg dokumentów kancelarii i ustalenie progów per typ pisma - z MateMatic.

---

## Moduł 3 - Transkrypcja rozmów (noScribe)

### Problem

Rozmowa z klientem, przesłuchanie, mediacja - wszystko warto mieć w transkrypcji przed wpisem do akt. Otter i podobne usługi robią to wygodnie i wysyłają nagranie do chmury US. Nagranie rozmowy z klientem to materiał objęty tajemnicą zawodową w stanie czystym.

### Kontekst prawny w skrócie

Dwie rzeczy naraz. Po pierwsze - transkrypcja musi zostać lokalnie (tajemnica zawodowa). Po drugie - samo nagrywanie rozmowy zwykle wymaga zgody klienta; bez niej powstaje problem niezależnie od narzędzia.

*Interpretacja MateMatic, nie stanowisko NRA ani KRRP.*

### Procedura krok po kroku

1. Zainstaluj noScribe (transkrypcja lokalna) i noScribeEdit (weryfikacja).
2. Przetestuj jakość na trzech nagraniach prawniczych po polsku - zmierz poziom błędów.
3. Ustal próg: poniżej 15% błędów - narzędzie do pracy; 15-25% - do pracy tylko z obowiązkową weryfikacją całości w noScribeEdit; powyżej 25% - dla polskiego odrzuć.
4. Wprowadź klauzulę zgody klienta na nagrywanie - przed rozmową, nie po.
5. Obieg: nagranie -> noScribe -> weryfikacja w noScribeEdit -> zapis w aktach.
6. Ustal, kto i kiedy kasuje surowe nagranie po sporządzeniu transkrypcji.

### Artefakt do pobrania

**Procedura transkrypcji + wzór klauzuli zgody klienta na nagrywanie** - gotowy akapit do dołączenia do umowy lub protokołu rozmowy.

### Pułapki

- Nagrywanie bez zgody - problem powstaje przed jakąkolwiek technologią.
- Transkrypcja traktowana jako protokół - to materiał roboczy, wymaga weryfikacji człowieka.
- Surowe nagrania zalegające bez polityki kasowania.

### Granica DIY / MateMatic

Test jakości i instalacja - samodzielnie. Klauzula zgody dopasowana do praktyki kancelarii i polityka cyklu życia nagrań - z MateMatic.

---

## Moduł 4 - E-podpis dokumentów (DocuSeal)

### Problem

NDA, pełnomocnictwa, ugody, umowy o świadczenie usług - codzienny obieg podpisów. DocuSign jest drogi i chmurowy. Kancelaria potrzebuje podpisu elektronicznego, który działa na jej serwerze i pod jej domeną.

### Kontekst prawny w skrócie

Trzeba rozróżnić formę dokumentową (art. 77² KC) od pisemnej i od formy z podpisem kwalifikowanym (art. 78¹ KC). Dla dużej części codziennej pracy kancelarii forma dokumentowa wystarcza - ale to ocena per typ dokumentu, nie założenie.

*Interpretacja MateMatic, nie stanowisko NRA ani KRRP.*

### Procedura krok po kroku

1. Postaw DocuSeal w Dockerze (docker compose).
2. Skonfiguruj Caddy z certyfikatem SSL i własną domeną kancelarii.
3. Przetestuj trzy typy dokumentów: NDA, pełnomocnictwo procesowe, umowę o świadczenie usług.
4. Sprawdź, czy forma dokumentowa wystarcza dla każdego z nich - jeśli nie, oznacz dokumenty wymagające podpisu kwalifikowanego.
5. Jeśli kancelaria potrzebuje podpisu kwalifikowanego - zweryfikuj integrację z polskim dostawcą (KIR, mObywatel, EuroCert, CenCert, PWPW).
6. Dodaj branding kancelarii - logo, domena, paleta.

### Artefakt do pobrania

**Procedura wdrożenia DocuSeal + arkusz walidacji formy** - tabela typów dokumentów kancelarii z kolumną „forma dokumentowa wystarcza / wymaga podpisu kwalifikowanego".

### Pułapki

- Założenie, że forma dokumentowa wystarcza zawsze - dla części czynności wymagana jest forma kwalifikowana.
- DocuSeal jest na licencji AGPL z dodatkowymi warunkami (Section 7b) - przed modelem, w którym hostuje go ktoś dla kancelarii, trzeba przejść warunki licencji.

### Granica DIY / MateMatic

Postawienie DocuSeal w Dockerze - dla administratora IT to kilka godzin. Walidacja formy prawnej per typ dokumentu i integracja eIDAS z polskim dostawcą - z MateMatic.

---

## Moduł 5 - Notatki i asystent AI lokalnie (Obsidian/AppFlowy + Cline)

### Problem

Kancelaria potrzebuje miejsca na wiedzę - notatki, bazy spraw, szablony - i coraz częściej asystenta AI do roboty. Notion to chmura US. Chmurowy asystent AI bez umowy powierzenia to dane klienta u dostawcy modelu.

### Kontekst prawny w skrócie

Baza wiedzy kancelarii zawiera dane osobowe i informacje objęte tajemnicą. Asystent AI uruchomiony lokalnie albo działający na modelu BYOK z umową powierzenia trzyma przetwarzanie pod kontrolą kancelarii.

*Interpretacja MateMatic, nie stanowisko NRA ani KRRP.*

### Procedura krok po kroku

1. Wybierz narzędzie do notatek: Obsidian (radca solo - prościej) albo AppFlowy (kancelaria z IT - bazy, współdzielenie).
2. Zainstaluj i ustaw strukturę: notatki, bazy spraw, szablony pism.
3. Jeśli kancelaria chce asystenta AI - zainstaluj Cline.
4. Domyślnie podłącz model lokalny (Ollama z Llama lub Mistral) - dane nie wychodzą.
5. Jeśli kancelaria świadomie wybiera model chmurowy - tylko z podpisaną umową powierzenia i wyłączeniem treningu.
6. Spisz politykę użycia dla zespołu: kiedy AI lokalne, kiedy BYOK, kiedy AI nie używamy w ogóle.

### Artefakt do pobrania

**Konfiguracja krok po kroku + szablon polityki użycia AI** - jednostronicowa polityka do podpisu przez zespół: dozwolone scenariusze, zakazane scenariusze, kto decyduje.

### Pułapki

- Asystent AI podłączony do modelu chmurowego „na szybko, do testu" - test też przetwarza prawdziwe dane.
- Brak spisanej polityki - zespół zgaduje, co wolno.

### Granica DIY / MateMatic

Notatki i model lokalny - samodzielnie. Polityka użycia AI dla zespołu i integracje na zamówienie (CRM kancelarii, własne narzędzia) - z MateMatic.

---

## Moduł 6 - Złożenie stacku i plan migracji

### Problem

Sześć narzędzi to nie sześć osobnych instalacji - to jeden zestaw, który ma działać razem i być wdrażany w rozsądnej kolejności. Kancelaria potrzebuje wiedzieć, od czego zacząć i ile to zajmie.

### Trzy poziomy stacku

- **Lite** (radca solo, 1-3 osoby): backup + OCR + transkrypcja. Fundament zero-cloud.
- **Standard** (kancelaria 5-20 osób): Lite + notatki/bazy + e-podpis.
- **Pro** (kancelaria 20-100 osób z IT): pełen zestaw + asystent AI + integracje na zamówienie.

### Procedura krok po kroku

1. Określ poziom stacku - Lite, Standard czy Pro - na podstawie wielkości i potrzeb kancelarii.
2. Sprawdź infrastrukturę: serwer, administrator IT, polityki bezpieczeństwa. Stack Lite i Standard - serwer 8 GB RAM, 4 CPU, 200 GB SSD wystarcza. Stack Pro z modelem lokalnym - potrzebny GPU.
3. Wdrażaj warstwami, nie naraz: najpierw fundament (backup + OCR), potem transkrypcja, potem notatki i e-podpis.
4. Po każdej warstwie - test na realnych dokumentach kancelarii.
5. Przeszkol zespół - osobno teoria (po co), osobno praca na narzędziach.
6. Spisz instrukcję techniczną dla administratora i politykę użycia dla zespołu.

### Artefakt do pobrania

**Harmonogram migracji 30/60/90 dni + checklista wyboru pakietu** - oś czasu z warstwami i kamieniami milowymi, plus krótki kwestionariusz „który poziom stacku dla mojej kancelarii".

### Pułapki

- Wdrażanie wszystkiego naraz - zespół się gubi, nic nie wchodzi w nawyk.
- Pominięcie testu na realnych dokumentach - narzędzie „działa" na przykładach, zawodzi na aktach.
- Szkolenie wyłącznie techniczne, bez „po co" - zespół wraca do starych nawyków.

### Granica DIY / MateMatic

Wybór poziomu i harmonogram - z tego podręcznika. Pełne wdrożenie produkcyjne - z instrukcją techniczną, szkoleniem zespołu, przeglądem czteroocznym i odpowiedzialnością za rezultat - to usługa wdrożeniowa MateMatic.

---

## Closer

Ten podręcznik daje Ci procedurę i artefakty. Wdrożenie sześciu warstw w działającej kancelarii, z odpowiedzialnością za ciągłość pracy i zgodność - to robimy z Tobą. Jeśli chcesz przejść od podręcznika do wdrożenia, napisz: kontakt@matematic.co.

## Changelog

- v1.0 (2026-05-25) - pierwsza publikacja. 7 modułów, 7 artefaktów do pobrania.
