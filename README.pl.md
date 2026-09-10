# Field Gulls

Field Gulls dodaje do Farming Simulator 25 animowane stada mew, które podążają za pracującymi narzędziami polowymi i żerują na świeżo obrobionej glebie.

> To repozytorium jest forkiem oryginalnego projektu [FS25_FieldGulls autorstwa sprkem](https://github.com/sprkem/FS25_FieldGulls). Fork jest utrzymywany w repozytorium [rdrygas/FS25_FieldGulls](https://github.com/rdrygas/FS25_FieldGulls) i zawiera dodatkowe poprawki oraz zmiany zachowania opisane poniżej.

## Opis

Mod ożywia prace polowe, przyciągając mewy do pługów, kultywatorów i siewników. Ptaki stopniowo nadlatują, przeszukują obszar obrobiony przez przypisane im narzędzie, lądują, aby żerować, i podrywają się do lotu, gdy pojazd znajdzie się zbyt blisko.

Mewy są aktywne wyłącznie w dzień i przy braku opadów. Rozpoczęcie pracy w nocy albo podczas deszczu, śniegu lub gradu nie aktywuje stada. Jeśli podczas aktywności stada zapadnie noc lub zaczną się opady, kolejne ptaki przestają się pojawiać i rozpoczyna się istniejąca, opóźniona sekwencja stopniowego odlotu.

## Założenia

- Farming Simulator 25 w wersji na PC/Mac.
- Mod działa ogólnie z pojazdami i narzędziami korzystającymi ze standardowych specjalizacji pługa, kultywatora lub siewnika.
- Nie wymaga konfiguracji konkretnej mapy ani zewnętrznych zależności.
- Zachowanie ptaków jest efektem wizualnym i nie zmienia plonów, wzrostu roślin, stanu gleby ani kosztów pracy.
- Tryb wieloosobowy jest zadeklarowany jako obsługiwany w `modDesc.xml`; aktualny stan weryfikacji opisano w sekcji [Zgodność](#zgodność).

## Funkcje

- Animowane mewy z zachowaniem obejmującym nadlatywanie, nurkowanie, żerowanie, poszukiwanie miejsca, ucieczkę i odlot.
- Obsługa pługów, kultywatorów i siewników używających standardowych obszarów roboczych FS25.
- Osobne strefy żerowania dla każdego narzędzia — mewy korzystają wyłącznie z terenu obrobionego przez przypisane narzędzie.
- Ucieczka ptaków przed zbliżającymi się pojazdami.
- Stopniowe pojawianie się i odlatywanie zamiast natychmiastowego dodawania lub usuwania całego stada.
- Ciągłe sprawdzanie pory dnia oraz opadów.
- Konfigurowalna wielkość stada, szansa pojawienia się, głośność oraz liczba jednocześnie aktywnych narzędzi.
- Angielska, polska, niemiecka i francuska lokalizacja menu ustawień.
- Lokalne zapisywanie ustawień w `modSettings/FieldGulls.xml`.

## Sposób działania

Gdy obsługiwane narzędzie rozpoczyna pracę, mod zapisuje jego świeżo obrobiony obszar. Jeżeli warunki środowiskowe są odpowiednie, limit aktywnych narzędzi nie został osiągnięty, a losowanie zakończy się powodzeniem, zaczyna nadlatywać stado liczące od 50% do 100% ustawionej maksymalnej liczby ptaków.

Każde stado pozostaje przypisane do własnego narzędzia. Ptaki wybierają miejsca żerowania z jego niedawno obrobionego obszaru i uciekają, kiedy pojazd zbliży się do ich pozycji. Zatrzymanie pracy, zniknięcie narzędzia, nadejście nocy lub rozpoczęcie opadów uruchamia opóźniony odlot, podczas którego ptaki opuszczają teren pojedynczo.

| Warunek | Rezultat |
|---|---|
| Obsługiwane narzędzie pracuje w dzień i bez opadów | Mod może aktywować stado zależnie od losowania oraz limitu aktywnych narzędzi. |
| Losowanie pojawienia się kończy się powodzeniem | Stopniowo pojawia się losowa liczba ptaków równa 50–100% ustawionego maksimum. |
| Losowanie pojawienia się kończy się niepowodzeniem | Dla tego narzędzia kolejne losowanie jest zablokowane przez 30 minut czasu rzeczywistego, niezależnego od czasu gry. |
| Praca rozpoczyna się w nocy albo podczas deszczu, śniegu lub gradu | Stado nie zostaje aktywowane i nie jest nakładana blokada za nieudane losowanie. |
| Podczas aktywności ptaków zapada noc lub zaczynają się opady | Pojawianie kolejnych ptaków zatrzymuje się i uruchamia się opóźniony, stopniowy odlot. |
| Narzędzie przestaje pracować | Po 15 sekundach stado rozpoczyna standardową sekwencję odlotu. |
| Narzędzie wznawia pracę przed upływem opóźnienia i warunki są odpowiednie | Oczekujący odlot zostaje anulowany, a stado pozostaje aktywne. |
| Pojazd zbliża się do żerującej mewy | Ptak porzuca miejsce żerowania i podrywa się do lotu. |
| Jednocześnie pracuje kilka obsługiwanych narzędzi | Każde stado korzysta wyłącznie ze strefy własnego narzędzia, z uwzględnieniem ustawionego limitu. |

## Instalacja

1. Pobierz archiwum wydania `FS25_FieldGulls.zip`.
2. Skopiuj je bez rozpakowywania do katalogu `mods` gry Farming Simulator 25.
3. Włącz **Field Gulls** podczas wczytywania lub tworzenia zapisu gry.

Typowa lokalizacja w systemie Windows:

```text
%USERPROFILE%\Documents\My Games\FarmingSimulator2025\mods
```

Plik `modDesc.xml` musi znajdować się bezpośrednio w katalogu głównym archiwum ZIP. Wewnątrz archiwum nie należy tworzyć dodatkowego katalogu nadrzędnego zawierającego wszystkie pliki moda.

## Konfiguracja

Otwórz menu ustawień gry i znajdź sekcję **Mewy polne**. Zmiany są zapisywane natychmiast i używane podczas kolejnych sesji.

| Ustawienie | Domyślnie | Dostępne wartości | Opis |
|---|---:|---|---|
| Głośność ptaków | 100% | 0–200% co 20% | Steruje głośnością stada. Wartość 0% wyłącza odgłosy ptaków. |
| Maksymalna liczba ptaków | 80 | 10–100 co 10, następnie 120–200 co 20 | Górny limit jednego stada. Rzeczywista liczba ptaków wynosi 50–100% tej wartości. |
| Pojawianie się ptaków | 70% | 10–100% co 10% | Szansa wybrania stada w chwili rozpoczęcia kwalifikującej się pracy. |
| Maks. aktywnych narzędzi | 2 | 1–10 lub Bez limitu | Ogranicza liczbę narzędzi, które mogą jednocześnie mieć aktywne stada. |

Plik ustawień znajduje się w profilu użytkownika Farming Simulator 25:

```text
modSettings/FieldGulls.xml
```

## Zgodność

- Gra: Farming Simulator 25 (`descVersion` 107).
- Obsługiwane rodzaje pracy: standardowe obszary robocze orki, kultywacji i siewu.
- Istniejące zapisy gry: zgodne; nowy zapis nie jest wymagany.
- Tryb wieloosobowy: zadeklarowany jako obsługiwany w metadanych moda, lecz fork nie dodaje jawnej synchronizacji sieciowej. Symulacja ptaków i ustawienia działają po stronie klienta, a zachowanie w multiplayerze nie zostało zweryfikowane.
- Znane konflikty: nieudokumentowane. Mody zastępujące te same wywołania specjalizacji mogą wpływać na zgodność.

## Znane ograniczenia

- Wykrywane są wyłącznie narzędzia udostępniające standardowe specjalizacje `Plow`, `Cultivator` lub `SowingMachine`.
- Szansa pojawienia się jest sprawdzana przy przejściu narzędzia ze stanu nieaktywnego do pracy. Jeśli praca rozpocznie się w złych warunkach i będzie trwała bez przerwy, samo nadejście dnia lub ustanie opadów nie aktywuje stada.
- Nieudane losowanie uruchamia 30-minutową blokadę, mimo że aktualna podpowiedź w menu gry mówi o jednej godzinie.
- Odlot wywołany zmianą warunków zachowuje standardowe 15-sekundowe opóźnienie, dlatego obecne ptaki nie znikają natychmiast po nadejściu nocy lub opadów.
- Bardzo duże stada i wysoki limit aktywnych narzędzi mogą obniżać wydajność.
- Zachowanie w trybie wieloosobowym nie zostało dotychczas zweryfikowane.

## Rozwiązywanie problemów

Jeżeli mod nie działa:

1. Sprawdź, czy `FS25_FieldGulls.zip` znajduje się bezpośrednio w katalogu `mods` gry.
2. Otwórz archiwum i upewnij się, że `modDesc.xml` znajduje się w jego katalogu głównym.
3. Sprawdź, czy mod został włączony dla bieżącego zapisu gry.
4. Przeprowadź próbę ze standardowym pługiem, kultywatorem lub siewnikiem w dzień i bez opadów.
5. Tymczasowo ustaw **Pojawianie się ptaków** na 100% i sprawdź, czy limit **Maks. aktywnych narzędzi** nie został osiągnięty.
6. Sprawdź `log.txt`, wyszukując wpisy zawierające `[FieldGulls]`, błędy Lua lub błędy ładowania moda.

Typowa lokalizacja logu w systemie Windows:

```text
%USERPROFILE%\Documents\My Games\FarmingSimulator2025\log.txt
```

Zgłoszenie problemu powinno zawierać wersję gry i moda, nazwę użytego narzędzia, pogodę i porę dnia, kroki odtwarzające problem oraz odpowiedni fragment pliku `log.txt`.

## Historia zmian

### Zmiany forka po wersji 1.0.0.1

- Ograniczono aktywację stad do dnia i pogody bez opadów.
- Dodano ciągłe sprawdzanie warunków środowiskowych podczas aktywności stada.
- Wykorzystano mechanizm stopniowego odlotu po nadejściu nocy lub rozpoczęciu opadów.
- Warunki środowiskowe nie uruchamiają już blokady przeznaczonej dla nieudanego losowania.

### 1.0.0.1 (projekt źródłowy)

- Ograniczono żerowanie każdego stada do ziemi obrobionej przez przypisane mu narzędzie.
- Dodano ustawienie maksymalnej liczby aktywnych narzędzi.
- Dodano polską lokalizację.

## Fork i autorzy

- Autor oryginalnego moda: **Ozz**.
- Oryginalne repozytorium: [sprkem/FS25_FieldGulls](https://github.com/sprkem/FS25_FieldGulls).
- Repozytorium i utrzymanie forka: [rdrygas/FS25_FieldGulls](https://github.com/rdrygas/FS25_FieldGulls).
- Autorzy polskiego tłumaczenia zapisani w projekcie źródłowym: **KITT3000** w `modDesc.xml` oraz **Ziuta** w pliku polskiej lokalizacji.

Ten fork nie jest przedstawiany jako oryginalne wydanie projektu źródłowego. Problemy dotyczące zmian w forku należy zgłaszać w repozytorium forka.

## Informacja o wykorzystaniu sztucznej inteligencji

Część kodu i dokumentacji forka przygotowano przy wsparciu OpenAI ChatGPT/Codex. Osoba utrzymująca projekt pozostaje odpowiedzialna za jego przegląd, testowanie, dystrybucję i licencjonowanie.

## Licencja

Repozytorium nie zawiera obecnie pliku licencji. O ile projekt źródłowy lub inne miarodajne źródło nie stanowi inaczej, prawa autora oryginału pozostają zastrzeżone.
