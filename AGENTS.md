# AGENTS.md - Praxis

Plik standardu [agents.md](https://agents.md) (Linux Foundation / Agentic AI Foundation) - kanoniczne instrukcje dla agentow AI pracujacych z tym repozytorium. Czytany natywnie przez Cursor, Codex (OpenAI), Jules (Google), Devin / Windsurf, Aider, Amp, Factory, GitHub Copilot.

## Cel projektu

**Praxis** to otwarta linia **przewodnikow praktycznych dla polskich kancelarii prawnych**, wydawana przez [MateMatic](https://matematicsolutions.com). Wiedza o bezpiecznym uzyciu AI w kancelarii ma byc dobrem wspolnym - to repo jest jej domem.

Dwa formaty:

- **Mapy** - zywe, przeszukiwalne zestawienia narzedzi i zasobow (np. mapa polskiego LegalTech AI).
- **Podreczniki** - proceduralne przewodniki krok po kroku z checklistami i artefaktami do pobrania.

Pierwszy podrecznik: **PX/03 - Stack zero-cloud dla kancelarii** ([przewodniki/px03-stack-zero-cloud/](./przewodniki/px03-stack-zero-cloud/)).

## Kontekst MateMatic (TWARDE OGRANICZENIA)

Repo prowadzi [MateMatic Solutions](https://matematicsolutions.com). Praxis ma trzy zasady redakcyjne ([README.md](./README.md)):

1. **Aktywne, nie statyczne** - to narzedzia pracy, nie zamrozone PDF-y.
2. **Subiektywne, nie obiektywne** - z jawnym komentarzem i ogladem MateMatic. Bez udawania "obiektywnego rankingu".
3. **Zywe, nie zamrozone** - wersjonowane, rozwijane z uwagami czytelnikow.

## Struktura repo

```
przewodniki/
  pxNN-slug/                 - kazdy podrecznik = osobny folder
    README.md                - tresc podrecznika
    artefakty/               - pliki do pobrania (checklisty, szablony)
    media/                   - obrazy, diagramy
README.md                    - landing repo + tabela podrecznikow
CONTRIBUTING.md              - jak zglosic poprawke / nowy podrecznik
LICENSE                      - CC BY-SA 4.0
```

Wersja webowa kazdego podrecznika: `https://matematicsolutions.com/akademia/pxNN-slug.html`.

## Build i test

Repo to czysty Markdown. Brak kompilacji.

"Test" = manualne przejscie podrecznika przez **2 archetypy kancelarii** (solo praktyk + zespol 10-osobowy) - jezeli ktorykolwiek krok nie jest wykonalny, to podrecznik jest zly.

Wersja webowa generowana jest przez repo `www-matematic` (private, deploy do matematicsolutions.com).

## Zasady pisania (CRITICAL)

- **Polski jezyk, ton MateMatic** - precyzyjny, spokojny, bez sales-marketingu. Patrz feedback `bw_style` w MEMORY operacyjnej.
- **Marko-pl 2x runda** przed kazdym commitem (zarzuty -> poprawki -> "ok") - ZAWSZE przed publikacja.
- **Humanizer-pl** dla finalnej polerki (anty-AI-slop).
- **Bez em-dash** - uzywaj zwyklego myslnika `-`. Nigdy `—` ani `–`.
- **Bez polskich znakow w commit messages** - konwencja organizacji.
- **Cytuj zrodla** - akt prawny (z CELEX dla UE), narzedzie (z linkiem do repo/strony), badanie (z DOI lub URL).
- **Checklisty wykonalne** - kazdy krok ma odpowiedz "tak/nie", bez "zastanow sie".

## Czego NIE robic (twarde reguly)

- **NIE udawaj obiektywnosci** - Praxis jest subiektywny z definicji. Pisz "MateMatic rekomenduje X poniewaz Y" zamiast "najlepsze narzedzie to X".
- **NIE wstawiaj sales-pitch Patrona / lpm-pl / matematic-readiness** w podrecznikach. Jezeli MateMatic produkt jest naturalnym przykladem - linkuj, ale tak samo neutralnie jak konkurencja.
- **NIE kopiuj 1:1 zewnetrznych tresci** bez atrybucji - CC BY-SA wymaga uznania autorstwa.
- **NIE commituj prawdziwych nazw kancelarii / klientow** w przykladach.

## Zrodla prawdy (kolejnosc czytania)

1. [README.md](./README.md) - landing + tabela podrecznikow
2. [CONTRIBUTING.md](./CONTRIBUTING.md) - zasady wspolpracy i format podrecznika
3. [przewodniki/pxNN-*/README.md](./przewodniki/) - tresc konkretnych podrecznikow
4. [LICENSE](./LICENSE) - CC BY-SA 4.0

## Kompatybilnosc agentow

Standard [AGENTS.md](https://agents.md). Dla Claude Code dodatkowo plik [CLAUDE.md](./CLAUDE.md).

## Licencja i atrybucja

- **CC BY-SA 4.0** - patrz [LICENSE](./LICENSE). Mozesz uzywac, kopiowac i rozwijac z uznaniem autorstwa MateMatic i na tej samej licencji.

Cytowanie: *MateMatic Solutions (2026), Praxis - przewodniki praktyczne dla polskich kancelarii, https://github.com/matematicsolutions/praxis, CC BY-SA 4.0.*
