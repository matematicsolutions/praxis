# Skill 04: Red-team pisma (co powie druga strona)

> Skill MateMatic do wgrania do Claude. Wersja DEMO lead magnetu.

## Po co to

Najgorszy moment na odkrycie słabości argumentu to pismo przeciwnika albo pytanie sądu. Ten skill każe Claude zaatakować Twoją własną tezę, zanim zrobi to ktoś, kto na tym skorzysta.

## Workflow (cztery role, po kolei)

1. **Builder.** Zbuduj najmocniejszą wersję Twojej tezy - najlepsze argumenty, najlepsze orzecznictwo, najczystsza struktura. Bez tego atak jest atakiem na słabszą wersję.
2. **Attacker.** Teraz zaatakuj ją bez litości: kontrargumenty, kontr-orzecznictwo, luki w stanie faktycznym, alternatywne wykładnie, słabe ogniwa łańcucha. Pytanie przewodnie: "gdyby to pismo chciało mnie pogrążyć, gdzie by uderzyło?".
3. **Synthesizer.** Pogódź: które ataki są realne i wymagają poprawki tezy, które da się odeprzeć, a które trzeba uczciwie ujawnić jako ryzyko.
4. **Verifier.** Kontrola końcowa: czy po poprawkach teza nadal się trzyma, czy żaden kontrargument nie został zamieciony pod dywan, czy powołane kontr-orzecznictwo jest prawdziwe (Skill 01).

## Format wyniku

`Najsilniejsza teza | Lista ataków (od najgroźniejszego) | Które wymagają zmiany pisma | Ryzyka do ujawnienia klientowi | Werdykt: czy gotowe do wysłania`.

## Kiedy odpalać

Tylko dla spraw wysokiej stawki (opinia, memo DD, M&A, pismo procesowe, rekomendacja do zarządu) - to kosztowne i niepotrzebne przy rutynie. Triage (Skill 02) podpowie, czy warto.

## Granice

DEMO. Pełna wersja (kontradyktoryjny pipeline z bramką kosztu i weryfikacją kontr-orzecznictwa) to stack MateMatic. Nie zastępuje porady prawnej ani osądu prowadzącego sprawę.

---
© MateMatic · Wiesław Mazur · matematicsolutions.com
