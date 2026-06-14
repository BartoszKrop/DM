# DATA MINING - TYPOWE PYTANIA EGZAMINACYJNE

## Baza typowych pytań na podstawie poprzednich egzaminów

---

## CZĘŚĆ 1: PYTANIA KONCEPCYJNE

### Q1: Opisz proces Data Mining
**Odpowiedź strukturalna:**
- Etap 1: **Zrozumienie problemu** - jakie pytanie chcemy odpowiedzieć?
- Etap 2: **Przygotowanie danych** - czyszczenie, standaryzacja
- Etap 3: **Eksploracja** - analiza statystyczna, wizualizacje
- Etap 4: **Modelowanie** - budowa i uczenie modelu
- Etap 5: **Ewaluacja** - czy model działa dobrze?
- Etap 6: **Wdrażanie** - użycie modelu w praktyce

**Czemu to ważne?** Każdy krok wpływa na ostateczny wynik. Bez dobrego przygotowania, najlepszy algorytm będzie słaby.

---

### Q2: Jakie są główne różnice między supervised i unsupervised learning?

| Aspekt | Supervised | Unsupervised |
|--------|-----------|--------------|
| **Dane treningowe** | Mają etykiety/odpowiedzi | Bez etykiet |
| **Cel** | Przewidzieć wartość docelową | Znaleźć strukturę w danych |
| **Przykład** | Regresja, Klasyfikacja | Klasteryzacja |
| **Ewaluacja** | Porównujemy z rzeczywistą odpowiedzią | Trudniejsza, metryki wewnętrzne |

**Sytuacja na egzaminie:** Opisz, co dostajesz w zbiorze danych i dlaczego to supervised/unsupervised.

---

### Q3: Regresja vs Klasyfikacja - kiedy które?

**Regresja:**
- Zmienna docelowa: **Ciągła** (liczby rzeczywiste)
- Przykład: Cena domu (100,000 - 500,000), temperatura (10.5°C)
- Algorytmy: Linear Regression, Decision Trees (regresja), Neural Networks
- Metryka: MSE, R²

**Klasyfikacja:**
- Zmienna docelowa: **Kategoryczna** (klasy/etykiety)
- Przykład: Spam (tak/nie), Gatunek (A/B/C), Choroba (zdrowy/chory)
- Algorytmy: Logistic Regression, SVM, Random Forest
- Metryka: Accuracy, Precision, Recall, F1

**Wskazówka:** Patrz na zmienną docelową - czy to liczba czy kategoria?

---

### Q4: Overfitting - co to jest i jak go poznać?

**Definicja:**
Model **zbyt dobrze dopasowany** do danych treningowych, memoryzuje szczegóły i szum zamiast nauczyć się wzorów.

**Jak poznać:**
- Doskonałe wyniki na danych treningowych (np. Accuracy 99%)
- **SŁABE wyniki na danych testowych** (np. Accuracy 60%)
- Duża różnica między train a test error = OVERFITTING!

**Dlaczego złe:**
Nie generalizuje - będzie słaby na nowych, nieznaych danych

**Jak unikać:**
1. **Pruning** - obcinanie drzewa
2. **Regularizacja** - penalizuj duże parametry (Ridge, Lasso)
3. **Early stopping** - zatrzymaj uczenie wcześniej
4. **Dropout** - losowo wyłączaj neurony
5. **Więcej danych** - szum się "rozmywa"
6. **Cross-validation** - testuj na różnych zbiorach

---

### Q5: Underfitting - kiedy mam na uwadze?

**Definicja:**
Model **zbyt prosty**, nie nauczył się wzorów w danych.

**Jak poznać:**
- Słabe wyniki na **OBU** danych treningowych i testowych
- Model nie konwerguje do sensownego rozwiązania

**Rozwiązanie:**
1. Bardziej skomplikowany model (więcej warstw w NN, głębjsze drzewo)
2. Więcej zmiennych/cech
3. Uczenie dłużej

---

### Q6: Bias-Variance Trade-off

```
       Error
        ▲
        │     Model C (dobry balans)
        │     /\
        │    /  \
        │   /    \
        │  /      \
        │ /        \
        │/          \
    ────┴─────────────────────────► Model Complexity
      Underfitting    Good         Overfitting
      (High Bias)   Balance     (High Variance)
```

**Bias:** Model jest systematycznie błędny
**Variance:** Model jest wrażliwy na szczegóły danych treningowych

- **Niedofit:** Wysoki bias, niska wariancja
- **Nadofit:** Niski bias, wysoka wariancja
- **Ideał:** Balans - pośrednia złożoność

---

## CZĘŚĆ 2: PYTANIA O ALGORYTMY

### Q7: Random Forest vs Single Decision Tree

**Single Tree:**
- ✅ Interpretowalne
- ❌ Może Overfitting
- ❌ Instabilny (małe zmiany = duże różnice)

**Random Forest:**
- ✅ Zmniejsza variance (wiele drzew, średnia/głos)
- ✅ Lepsze uogólnianie
- ✅ Feature importance
- ❌ Mniej interpretowalne
- ❌ Drożej obliczeniowo

**Odpowiedź:** Jeśli chcę czegoś szybkiego i zrozumiałego → Single Tree. Jeśli chcę maksymalnej dokładności → Random Forest.

---

### Q8: SVM - kiedy używać?

**Zalety:**
- ✅ Ekscelentny dla **klasyfikacji binarnej**
- ✅ Efektywny w wysokiej liczbie wymiarów
- ✅ Kernel trick pozwala na nieliniowe granice

**Wady:**
- ❌ Czarny pudełek (trudno zinterpretować)
- ❌ Klasyfikacja wieloklasowa jest trudniejsza
- ❌ Droższy na dużych zbiorach danych (O(n²) lub O(n³))

**Kiedy używać:**
- Binarna klasyfikacja
- Średnia liczba danych
- Nie potrzebujesz interpretacji
- Dużo cech

---

### Q9: Porównaj K-Means, Hierarchical Clustering i DBSCAN

| Cecha | K-Means | Hierarchical | DBSCAN |
|-------|---------|-------------|---------|
| **Kształt klastru** | Kuliste | Dowolny | Dowolny |
| **K parametr** | Trzeba wybrać | Nie | Nie |
| **Wynik** | Płaska partycja | Dendrogram (hierarchia) | Gęste regiony |
| **Szum/Outliers** | Przypisuje wszędzie | Przypisuje wszędzie | Oznacza jako szum |
| **Prędkość** | Szybki | Wolny (O(n²)) | Zależy od parametrów |
| **Kiedy** | Szybka analiza | Eksploracyjna | Szukasz struktur gęstości |

---

### Q10: Neural Networks - jak się uczy?

**Forward Pass (przód):**
1. Dane wejściowe
2. Przechodzą przez warstwy (transformacje)
3. Wyjście (predykcja)

**Oblicz Error (Loss):**
- Porównaj przewidywanie z rzeczywistością
- Loss = odległość od prawdy

**Backward Pass (tył - Backpropagation):**
1. Błąd idzie wstecz przez sieć
2. Obliczamy gradient (kierunek i siłę zmiany)
3. Updatujemy wagi: waga = waga - learning_rate * gradient

**Powtarzaj:** Iteracje aż do zbieżności

**Hiperparametry do uważania:**
- Learning rate: Zbyt wysoki = divergence, zbyt niski = powolne
- Batch size: Większy = stabilniejszy ale wolniejszy
- Liczba warstw/neuronów: Więcej = bardziej elastyczne ale niebezpieczne dla overfitting

---

## CZĘŚĆ 3: PYTANIA PRAKTYCZNE

### Q11: Masz zbiór z brakującymi wartościami. Co robisz?

**Opcje:**

1. **Usunąć wiersze z brakami**
   - ✅ Proste
   - ❌ Tracimy dane

2. **Usunąć kolumny (zmienne) z brakami**
   - ✅ Proste
   - ❌ Tracimy cechy

3. **Imputation (uzupełnianie):**
   - **Mean/Median:** Średnia wartość - proste, może zafałszować rozkład
   - **KNN:** Wartość od podobnych obserwacji - inteligentne
   - **Model:** Uczyć model do przewidzenia brakujących - dobrze ale drożej

**Czym się kierować:**
- Ile brakuje? (5% → usuń, 30% → imputation)
- Czy braki są losowe czy systematyczne?
- Co ma więcej sensu biznesowo?

---

### Q12: Masz outliers. Co robisz?

**Identyfikacja:**
- Z-score: |x - mean| > 3*std
- IQR: x < Q1 - 1.5*IQR lub x > Q3 + 1.5*IQR
- Wizualizacja: boxplot, scatter plot

**Decyzja:**

1. **Usunąć?**
   - ✅ Jeśli to błąd/szum
   - ❌ Jeśli to ważna obserwacja

2. **Zachować?**
   - ✅ Jeśli to rzeczywiste dane
   - ❌ Może zniekształcić model

3. **Transformować?** (log, sqrt)
   - ✅ Zmniejsza wpływ bez usuwania
   - ❌ Trudniejsza interpretacja

**Rada:** Zawsze zbadaj dlaczego jest outlier zanim go usuniesz!

---

### Q13: Standaryzacja czy Normalizacja?

**Standaryzacja (Z-score):**
```
X_std = (X - mean) / std
Wynik: ~[-2, 2]
```

**Normalizacja (Min-Max):**
```
X_norm = (X - min) / (max - min)
Wynik: [0, 1]
```

**Którą wybrać:**
- **Zawsze dla:** KNN, SVM, Neural Networks (wrażliwe na skalę!)
- **Opcjonalnie dla:** Trees (skala nie ma znaczenia)
- **Kiedy porównujesz na tej samej skali:** Normalizacja
- **Kiedy chcesz zachować rozkład:** Standaryzacja

---

### Q14: Selekcja zmiennych - jakie zmienne wybrać?

**Filter Methods (szybkie):**
1. **Korelacja ze zmienną docelową** - weź zmienne najsilniej skorelowane
2. **Chi-square test** - dla zmiennych kategorycznych
3. **Mutual Information** - wspólna informacja

```
Proces: Oblicz score dla każdej zmiennej → Usuń te z niskim score
```

**Wrapper Methods (dokładne):**
```
Forward Selection:
1. Zacznij z pustawą
2. Dodaj zmienną która daje najlepszy wynik
3. Powtarzaj, aż nie ma polepszenia

Backward Elimination:
1. Zacznij ze wszystkimi
2. Usuwaj zmienną która daje najmniej polepszenia
3. Powtarzaj
```

**Embedded (wbudowana w model):**
- Tree-based Feature Importance: patrzę które zmienne są używane
- Regularization (Ridge/Lasso): Automatycznie zmniejsza/zeruje mniej ważne

**Wskazówka:** Zacznij od Filter (szybkie), potem Wrapper jeśli będzie czas.

---

### Q15: Model słabo generalizuje. Co sprawdzić?

**Diagnoza:**
- Dużo parametrów vs mało danych? → OVERFITTING
- Model zbyt prosty? → UNDERFITTING
- Zły podział train/test? → Może data leakage
- Klasy niezbalansowane? → Metryka powinna być F1/AUC, nie Accuracy

**Checklist:**
- ✅ Czy preprocessing był poprawny? (brakujące, outliers, skalowanie)
- ✅ Czy używasz cross-validation? (żeby mieć pewność)
- ✅ Czy masz wystarczająco danych?
- ✅ Czy wszystkie zmienne są istotne?
- ✅ Czy klasyfikacja jest zbilansowana?
- ✅ Czy hiperparametry są dobrze dobrane?

---

## CZĘŚĆ 4: EWALUACJA MODELU

### Q16: Kiedy Accuracy jest zła metryką?

**Problem z Accuracy:**
```
Zbiór: 1000 próbek, 950 negatywnych, 50 pozytywnych
Model zawsze mówi "negatywny"
Accuracy = 950/1000 = 95%  ← Wygląda dobrze!
Ale złapaliśmy ZERO pozytywnych!
```

**Kiedy zła:**
- Niezbalansowane klasy
- Jedna klasa jest ważniejsza (np. choroba, oszustwo)
- False Positives lub False Negatives mają inny koszt

**Lepsze metryki:**
- **F1 Score** - balansuje Precision i Recall
- **Precision** - jeśli False Positives są kosztowne
- **Recall** - jeśli False Negatives są kosztowne
- **AUC-ROC** - pokazuje trade-off

---

### Q17: Precision vs Recall - jaką wybrać?

**Precision = Jak dokładne są nasze "TAK"?**
```
TP / (TP + FP)
```
- Ważne gdy: False Positive jest drogi (np. spam filter - nie chcemy usunąć ważnych maili!)
- **High Precision** = gdy mówimy "TAK", możesz być pewny

**Recall = Ile "TAK" złapaliśmy?**
```
TP / (TP + FN)
```
- Ważne gdy: False Negative jest drogi (np. nowotwór - nie chcesz przegapić chorego!)
- **High Recall** = nie przegapisz żadnego "TAK"

**Praktyka:**
- Spam filter: Wysokie Precision (nie chcemy stracić maili)
- Diagnostyka medyczna: Wysokie Recall (nie przegap pacjentów)
- Czarna lista: Środek (coś False Positives, ale nie za wiele False Negatives)

---

### Q18: ROC Curve - co to pokazuje?

```
TPR (True Positive Rate)
▲
1 ├─────────┐
  │        /│ Doskonały klasyfikator
  │      /  │
  │    /    │
  │  /      │ Dobry klasyfikator
  │/        │
0 └────────┤─────────► FPR (False Positive Rate)
           └─────────► 1
```

**Interpretacja:**
- Diagonala (od (0,0) do (1,1)) = klasyfikator bez wartości (losowy)
- Im wyżej lewa strona, tym lepiej
- **AUC (Area Under Curve):** 0-1
  - 1.0 = Doskonały
  - 0.5 = Losowy
  - <0.5 = Gorzej niż losowy (może źle przewidzieć)

**Kiedy używać:** Niezbalansowane klasy!

---

## CZĘŚĆ 5: STRATEGIA EGZAMINACYJNA

### Jeśli dostaniesz problem do rozwiązania:

#### Krok 1: CZYTAJ UWAŻNIE (1 minuta)
```
- Jaki jest cel? (przewidzieć co?)
- Ile danych?
- Jakie są kolumny?
- Czy jest zmienna docelowa?
```

#### Krok 2: KATEGORYZUJ (1 minuta)
```
- Supervised czy unsupervised?
- Regresja czy klasyfikacja?
- Kolumna docelowa: ciągła czy kategoryczna?
```

#### Krok 3: WYBRANIE ALGORYTMU (2 minuty)
```
Odpowiedz na pytania:
□ Potrzebuję interpretacji? → Tree
□ Maksymalna dokładność? → Ensemble
□ Binarna klasyfikacja? → SVM lub LR
□ Klasteryzacja? → K-Means lub DBSCAN
□ Obrazy/sekwencje? → CNN/RNN
□ Dużo cech? → SVM z RBF lub NN
```

#### Krok 4: PREPROCESSING (2 minuty)
```
□ Brakujące wartości?
□ Outliers?
□ Potrzebujesz standaryzacji? (SVM, NN, KNN - TAK!)
□ Selekcja zmiennych?
```

#### Krok 5: METRYKA (1 minuta)
```
□ Niezbalansowane klasy? → F1/AUC nie Accuracy
□ Regresja? → RMSE lub R²
□ Klasyfikacja? → Precision/Recall/F1 (zależy od problemu)
```

#### Krok 6: WALIDACJA (1 minuta)
```
□ Cross-validation? (7-fold, 10-fold)
□ Jak sprawdzić overfitting?
□ Jak porównać z baseline?
```

#### Krok 7: DYSKUSJA (2 minuty)
```
□ Dlaczego wybrałeś TO?
□ Jakie są wady tego podejścia?
□ Co byś zmienił?
□ Alternatywy?
```

---

## CZĘŚĆ 6: SŁOWNIK TERMINÓW

| Termin | Wyjaśnienie |
|--------|------------|
| **Features** | Zmienne wejściowe |
| **Target** | Zmienna docelowa (do przewidzenia) |
| **Training Data** | Dane do uczenia modelu |
| **Test Data** | Dane do ewaluacji (niewidoczne podczas uczenia) |
| **Validation Data** | Dane do strojenia hiperparametrów |
| **Overfitting** | Model zbyt dopasowany, słaby na nowych danych |
| **Underfitting** | Model zbyt prosty, słaby wszędzie |
| **Cross-validation** | Wielokrotne podziały train/test |
| **Grid Search** | Testowanie kombinacji parametrów |
| **Learning Curve** | Wykres błędu vs ilość danych |
| **Confusion Matrix** | Tabela TP, FP, FN, TN |
| **Regularization** | Penalizacja za skomplikowane modele |
| **Dropout** | Losowe wyłączanie neuronów |
| **Activation Function** | ReLU, Sigmoid, Tanh - dodaje nieliniowość |
| **Kernel Trick** | Transformacja do wyższych wymiarów bez eksplicitnego obliczania |
| **Ensemble** | Kombinacja wielu modeli |
| **Feature Scaling** | Standaryzacja/Normalizacja |

---

## OSTATECZNE WSKAZÓWKI

✅ **Do zapamiętania:**
- Każdy algorytm ma swoje zastosowanie
- Nie ma jednego najlepszego - zależy od problemu
- Trade-off'y są wszędzie (szybkość vs dokładność, prostota vs elastyczność)
- Preprocessing i selekcja zmiennych mogą być ważniejsze niż wybór algorytmu
- Cross-validation to Twój najlepszy przyjaciel!

❌ **Unikaj:**
- "Zawsze używam SVM" - zależy od problemu!
- Porównywania modeli na tej samej mierze (Accuracy dla niezbalansowanych)
- Testowania na danych treningowych
- Nie skalowania danych dla SVM/NN
- Zapominania o baseline (prosty model na porównanie)

🎯 **Na egzaminie:**
- Wyjaśnij swoje myślenie
- Uzasadnij każdą decyzję
- Bądź przygotowany na "co jeśli?" pytania
- Pokaż znowu problem z wieloma aspektami
- Pamiętaj: Process > Results

**Powodzenia! 💪**
