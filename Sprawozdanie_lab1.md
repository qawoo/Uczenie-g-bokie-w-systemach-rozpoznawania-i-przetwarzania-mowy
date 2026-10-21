# Sprawozdanie laboratoryjne — zajęcia 1

**Przedmiot:** Uczenie głębokie w systemach rozpoznawania i przetwarzania mowy  
**Zajęcia nr / temat:** 1 — Sekwencje i sygnał mowy: od fali dźwiękowej do reprezentacji  
**Autor / grupa:** Piotr Wójtowicz  
**Data:** 21.10.2026

## 1. Cel ćwiczenia

Celem było przedstawienie trzech nagrań mowy (samogłoska, wyraz, zdanie) za pomocą fali dźwiękowej, spektrogramu log-mel i współczynników MFCC. Sprawdziłem też, jak parametry `n_fft` i `hop_length` wpływają na wygląd spektrogramu.

## 2. Metoda i implementacja

Do analizy wykorzystano Python i biblioteki `librosa`, `numpy`, `matplotlib`. Nagrania mają zostać wczytane do 16 kHz w trybie mono. Ustawienia bazowe to `n_fft=512`, `hop_length=160`, 64 pasma mel i 13 współczynników MFCC. Dla długości okna porównuję 256, 512 i 1024 próbek przy kroku 160. Dla kroku porównuję 80, 160 i 320 próbek przy oknie 512.

Pełny kod znajduje się w `Lab1_przetwarzanie_mowy.ipynb`. Notatnik po wgraniu nagrań zapisuje również gotowe sprawozdanie z liczbowymi wynikami i dziewięcioma wykresami.

## 3. Wyniki

Trzeba jeszcze wgrać trzy własne nagrania, których nie było w przesłanych materiałach. Z tego powodu nie wpisuję fikcyjnych czasów trwania, wartości MFCC ani nie pokazuję wykresów innych sygnałów jako wyników własnego pomiaru.

| Nagranie | Czas trwania | Log-mel | MFCC | Wykresy |
|---|---|---|---|---|
| Samogłoska | po wgraniu WAV | 64 × T | 13 × T | generowane w notatniku |
| Wyraz | po wgraniu WAV | 64 × T | 13 × T | generowane w notatniku |
| Zdanie | po wgraniu WAV | 64 × T | 13 × T | generowane w notatniku |

Przy 16 kHz okno 256 próbek ma 16 ms, 512 próbek ma 32 ms, a 1024 próbki mają 64 ms. Kroki 80, 160 i 320 próbek odpowiadają 5, 10 i 20 ms. **T** oznacza liczbę ramek — zmienia się zależnie od długości nagrania i ustawionego kroku.

## 4. Analiza i interpretacja

Na wykresie fali można wskazać głośniejsze fragmenty oraz przerwy. Log-mel pokazuje rozłożenie energii w pasmach częstotliwościowych w czasie. MFCC opisuje kształt widma za pomocą 13 współczynników; jego oś pionowa nie oznacza częstotliwości.

W jednostajnie wypowiadanej samogłosce można oczekiwać bardziej stabilnego obrazu cech niż w wyrazie, w którym zmieniają się głoski. Zdanie może zawierać więcej przejść i przerw. Konkretne przedziały czasowe i różnice pomiędzy trzema nagraniami należy odczytać z wygenerowanych wykresów po wgraniu nagrań.

Zwiększenie `n_fft` poprawia rozdzielanie sąsiadujących częstotliwości, ale rozmywa nagłe zmiany w czasie. Zmniejszenie `hop_length` zwiększa liczbę ramek, ale nie skraca okna. Dla tych samych nagrań przy kroku 80 powinno więc wyjść około dwa razy więcej kolumn niż przy kroku 160, a przy kroku 320 — około dwa razy mniej.

## 5. Wnioski

1. Przebieg czasowy ułatwia ocenę głośności i przerw, ale nie pokazuje bezpośrednio słów.
2. Log-mel przedstawia zmiany energii w pasmach mel, a MFCC daje krótszy opis widma.
3. Dłuższe okno poprawia rozdzielczość częstotliwościową kosztem rozdzielczości czasowej.
4. Krótszy krok zwiększa liczbę ramek i szczegółowość próbkowania sygnału w czasie.
5. Końcowe porównanie własnych nagrań wymaga ich odsłuchania i analizy konkretnych fragmentów na wykresach.
