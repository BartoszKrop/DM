# DATA MINING - PRAKTYCZNE PRZYKŁADY I DRZEWA DECYZYJNE

## Jak podejść do typowych problemów

---

## SCENARIUSZ 1: Przewidywanie ceny domu

### Problem
```
Mamy dane o domach: powierzchnia, liczba pokoi, lokalizacja, rok budowy, itd.
Celem: Przewidzieć cenę
```

### Analiza problemu
- ✅ Mamy zmienną docelową (cena)
- ✅ Znamy wartości docelowe dla danych treningowych
- 📊 Zmienna docelowa jest **CIĄGŁA** (liczby rzeczywiste)
- → **REGRESJA**

### Wybór algorytmu - drzewo decyzyjne

```
Czy relacja między zmiennymi jest liniowa?
├─ TAK → Linear Regression
├─ NIEZNANE → Spróbuj oba
└─ NIE, wiele wzorów → Polynomial Regression, Decision Tree, Random Forest

Ile masz danych?
├─ <1000 → Linear Regression, SVM
├─ 1000-100000 → Decision Tree, Random Forest
└─ >100000 → Gradient Boosting (szybszy)

Potrzebujesz interpretacji?
├─ TAK → Single Decision Tree, Linear Regression
└─ NIE, maksymalnie dokładniego → Random Forest, Gradient Boosting
```

### Preprocessing
- [ ] Standaryzacja? 
  - Linear Regression: NIE (ale nie boli)
  - SVM: TAK
  - Trees: NIE
- [ ] Outliers - domu za 1 miliarda? Sprawdzić lub usunąć
- [ ] Brakujące - średnia/mediana rozsądna dla ciągłych
- [ ] Selekcja zmiennych - które cechy rzeczywiście wpływają na cenę?

### Metryka
- **R²** - ile procent wariancji wyjaśniasz? (0-1, im wyżej tym lepiej)
- **RMSE** - pierwiastek średniokwadratowego błędu (w jednostkach ceny)
- Czemu nie Accuracy? Bo to nie klasyfikacja!

### Walidacja
```python
Pseudokod:
for i in range(10):  # 10-fold CV
    train_set = dane bez i-tego foldu
    test_set = i-ty fold
    
    model = RegresjaLiniowa()
    model.fit(train_set)
    R2_score = model.evaluate(test_set)
    
Średnia R2 = średnia z 10 wyników
```

---

## SCENARIUSZ 2: Klasyfikacja emaili - Spam czy Nie?

### Problem
```
E-maile z tekstem, chcemy: SPAM (1) czy LEGIT (0)
```

### Analiza problemu
- ✅ Zmienna docelowa: TAK/NIE (binarna)
- → **KLASYFIKACJA BINARNA**

### Wybór algorytmu

```
Czy potrzebujesz interpretacji?
├─ TAK → Logistic Regression, Decision Tree
├─ ŚRODEK → Naive Bayes, Linear SVM
└─ NIE → Random Forest, SVM z RBF, Neural Network

Klasy zbilansowane?
├─ TAK → Accuracy jest OK
└─ NIE → Musimy F1, Precision, Recall, AUC!

Ile danych i cech?
├─ Mały zbiór → Logistic Regression
├─ Średni → SVM, Random Forest
└─ Duży → Neural Network, Gradient Boosting
```

### Preprocessing
- [ ] Brakujące teksty - czy mogą być?
- [ ] Normalizacja tekstu (lowercase, interpunkcja)
- [ ] Feature engineering:
  - Długość tekstu
  - Liczba wyrazów
  - Liczba dużych liter
  - Słowa klucze (FREE, CLICK, $$$)
- [ ] Bag of Words / TF-IDF (dla tekstu)
- [ ] Standaryzacja liczb

### Problem: Niezbalansowane klasy
```
Przykład:
5000 emaili → 4900 legit, 100 spam

Model "zawsze legit" → Accuracy 98% ale BEZUŻYTECZNY!

Rozwiązanie:
- F1 Score zamiast Accuracy
- Precision: z emaili które zaznaczyliśmy jako spam, ile faktycznie jest?
- Recall: ile spamów rzeczywiście złapaliśmy?
```

### Metryka
- **F1 Score** - harmonijna średnia Precision i Recall
- **AUC-ROC** - pokazuje trade-off
- Czemu? Accuracy będzie zawsze wysoki ze względu na niezbalans

### Macierz błędów (Confusion Matrix)
```
          Przewidywany
          SPAM  LEGIT
Rzeczywisty
SPAM      TP     FN      (FN = przegapiony spam - ZŁE!)
LEGIT     FP     TN      (FP = fałszywy alarm - złe ale mniej)

Jakie są konsekwencje?
- FN (spam przejdzie): Zły, ale ludzki przywyknie
- FP (legit w spam): Bardzo zły! Użytkownik nie zobaczy ważnego maila

→ Wymaga High Precision (pewny zanim powiem SPAM)
```

---

## SCENARIUSZ 3: Segmentacja klientów

### Problem
```
Mamy dane o tysiącach klientów (wiek, zakupy, lokalizacja...)
Chcemy: Podzielić na grupy (segmenty) do targetowania
```

### Analiza problemu
- ❌ Brak zmiennej docelowej
- → **KLASTERYZACJA / SEGMENTACJA**

### Wybór algorytmu

```
Jakie chcemy klastry?
├─ Kuliste, wyrówniejsze → K-Means
├─ Hierarchia, możliwość "przecięcia" → Hierarchical Clustering
└─ Dowolny kształt, szum → DBSCAN

Czy znamy liczbę segmentów?
├─ TAK → K-Means (K znane)
└─ NIE → Hierarchical (wizualizuj dendrogram) lub DBSCAN
```

### K-Means - How to choose K?

#### Metoda 1: Elbow Method
```
For k in range(1, 10):
    model = KMeans(k)
    inertia = model.inertia_  # suma odległości do centroidów
    plot(k, inertia)

Szukaj "łokcia" gdzie zmiana się ustabilizuje
```

#### Metoda 2: Silhouette Score
```
Dla każdego k:
    silhouette = silhouette_score(dane, labels)
    
Wybierz k z najwyższym score (-1 do 1)
```

### Preprocessing
- [ ] Standaryzacja - OBOWIĄZKOWE!
  - (wiek 25-80 vs zarobki 100k-1M - różne skale!)
- [ ] Usunąć zmienne bezużyteczne
- [ ] Zmienne kategoryczne → OneHotEncoding

### Interpretacja wyników

```
Otrzymałam 3 segmenty:
- Segment A: Średnia wieku 25, wydatki 100/miesiąc
  → Młodzi, budzet-conscious
  
- Segment B: Średnia wieku 55, wydatki 5000/miesiąc
  → Starsi, high-value customers
  
- Segment C: Średnia wieku 30, wydatki 500/miesiąc
  → Młodsze profesjonaliści

Strategia marketingu:
- A: Promocje, bundle deals
- B: Premium products
- C: Lifestyle products
```

### Metryka
- **Silhouette Score** - jak dobrze punkty pasują do klastrów?
- **Davies-Bouldin Index** - separacja między klastrami
- **Inertia** - tylko do szukania K, nie do porównania algorytmów

---

## SCENARIUSZ 4: Detekcja anomalii

### Problem
```
Transakcje bankowe - szukamy oszustw (anomalii)
```

### Podejście 1: Unsupervised (brak etykiet)
- **One-class SVM** - nauczaj się "normalnych", flaguj odchylenia
- **Isolation Forest** - szuka punktów izolowanych
- **DBSCAN** - punkty "Same" to anomalie

### Podejście 2: Supervised (są etykiety)
- **Random Forest** - jak wyżej, ale z klasyfikacją
- **Neural Network** - autoencoder (uczysz się reprezentacji, anomalie mają duży błąd)

### Preprocessing
- Standaryzacja obowiązkowa!
- Może być więcej outlierów niż w normalnym problemie

### Metryka
```
Oszustwo to MAŁY procent (np. 0.1%)
→ Recall ważny! (nie chcesz przegapić oszusta)
→ AUC lepszy niż Accuracy
```

---

## SCENARIUSZ 5: Predykcja churn (odejścia klientów)

### Problem
```
Dane o klientach (jak długo trwa kontrakt, ile ma wydatków...)
Chcemy: Przewidzieć czy klient nas opuści
```

### Analiza problemu
- Zmienna docelowa: CHURN (Tak/Nie)
- → **KLASYFIKACJA BINARNA**
- Problem: Zwykle mało churn'ów (5-20% bazowych)
- → Niezbalansowana klasyfikacja!

### Rozwiązania dla niezbalansu

#### Metoda 1: Class Weights
```python
model = RandomForest(class_weight='balanced')
# Daje wyższą wagę klasie mniejszościowej
```

#### Metoda 2: Oversampling
```python
# SMOTE - generuj nowe przykłady churn'u syntetycznie
from imblearn.over_sampling import SMOTE
smote = SMOTE()
X_train, y_train = smote.fit_resample(X_train, y_train)
```

#### Metoda 3: Undersampling
```python
# Usuń przykłady nie-churn'u
# Ryzyko: stracimy informację
```

### Strategia

```
1. Przygotuj dane
   - OneHot encoding dla kategorii
   - Standaryzacja
   - Selekcja zmiennych (czego klient zazwyczaj unika?)

2. Rozwiąż niezbalans (SMOTE lub class_weights)

3. Testuj algorytmy
   - Logistic Regression (baseline)
   - Random Forest
   - Gradient Boosting

4. Ewaluuj na metrykach istotnych
   - Recall dla churn'u (nie chcesz przegapić)
   - Precision też ważna (nie chcesz "straszy" klientów)
   - F1 Score
   - AUC-ROC

5. Intepretacja
   - Feature importance - co najpyroduje customer'ów?
   - Jaki jest "profil" odchodzącego klienta?
```

---

## SCENARIUSZ 6: Rekomendacje (Collaborative Filtering)

### Problem
```
Netflix: Wiemy ile gwiazdek dał użytkownik każdemu filmowi
Chcemy: Przewidzieć rating dla filmów, które nie widział
```

### Podejście
- **Matriz Factorization** (nie omawialiśmy, ale fajnie wiedzieć)
- **Neural Networks** (autoencoder)
- **Similarity-based** - szukamy użytkowników podobnych do ciebie, patrzę ich oceny

---

## DRZEWA DECYZYJNE - PRAKTYCZNA APLIKACJA

### Jak czytać drzewo decyzyjne?

```
                 [wiek <= 30?]
                /              \
              TAK               NIE
             /                    \
      [zarobki<50k?]          [zarobki<100k?]
       /         \             /          \
     TAK         NIE         TAK          NIE
    /             \          /              \
STUDENT      [wiek<=25?]   NORMAL        PREMIUM
              /      \
            TAK      NIE
           /          \
        EARLY      PROFESSIONAL
```

### Jak interpretować węzły

```
Każdy węzeł zawiera:
- Pytanie (split)
- Ile próbek trafia tutaj
- Rozkład klas (jak wiele TAK vs NIE)
- Dominująca klasa (decyzja jeśli liść)

Przykład:
[income <= 50000]
samples = 300
value = [100, 200]  (100 poor, 200 not poor)
class = not poor    (większość)
```

---

## FEATURE IMPORTANCE - INTERPRETACJA

### Dla Tree-based modeli (Trees, Random Forest, Boosting)

```python
model = RandomForest()
model.fit(X, y)

feature_importance = model.feature_importances_
# [0.3, 0.25, 0.2, 0.15, 0.1]  dla 5 zmiennych

Top 3 features:
1. Feature 0: 30% ważności
2. Feature 1: 25% ważności
3. Feature 2: 20% ważności

Interpretacja: Features 0, 1, 2 odpowiadają za większość decyzji modelu
```

### Dla Linear models (Linear Regression, Logistic Regression)

```python
model = LogisticRegression()
model.fit(X, y)

coefficients = model.coef_[0]
# [0.5, -0.3, 0.8, 0.1, -0.2]

Interpretacja:
- Pozytywny = zwiększa szansę na klasę +
- Ujemny = zmniejsza szansę
- Większa wartość = większy wpływ
```

---

## PERMUTATION IMPORTANCE

### Idea
```
Jeśli zmienne są rzeczywiście ważne, to jej przemieszanie
powinna znaleźć wyniki

1. Zbiór testowy A: train model, test na danych testowych → Score 0.85
2. Permutacja feature X w zbiorze testowym
3. Test na permutowanym zbiorze → Score 0.82
4. Spadek = 0.03 = importance of X
```

### Zaleta
- Niezależna od modelu (działa dla każdego!)
- Uwzględnia interakcje między zmiennymi

---

## INTERPRETACJA REGRESJI

```
Model: price = 100000 + 200*sqm + 50000*rooms - 1000*age

Interpretacja:
- Dla każdego m² dodaj 200 do ceny
- Każdy pokój to +50k
- Każdy rok wieku odejmuje 1k (dom starzeje się)

Ale! To linear model - może być niedokładne dla skrajnych wartości!
```

---

## OSTATNI CHECKLIST PRZED EGZAMINEM

### Generalnie zawsze robisz:
- [ ] Przeczytaj problem dokładnie
- [ ] Zidentyfikuj typ zadania (supervised/unsupervised, regresja/klasyfikacja)
- [ ] Preprocessing (brakujące, outliers, skalowanie)
- [ ] Selekcja zmiennych
- [ ] Wybór algorytmu(ów)
- [ ] Cross-validation
- [ ] Odpowiednia metryka
- [ ] Interpretacja wyników
- [ ] Dyskusja limitów i alternativ

### Jeśli masz problem z overfitting:
1. Zmniejsz model (mniej warstw, mniej drzewa)
2. Regularizacja (Ridge, Lasso, Dropout)
3. Więcej danych
4. Early stopping
5. Pruning (dla drzew)

### Jeśli masz problem z underfitting:
1. Bardziej skomplikowany model
2. Więcej zmiennych/cech
3. Uczenie dłużej
4. Zmień algorytm na bardziej elastyczny

### Jeśli masz niezbalansowane klasy:
1. Zmień metrykę (F1, AUC zamiast Accuracy)
2. Class weights
3. SMOTE oversampling
4. Threshold adjustment

---

## CHEAT SHEET - ALGORYTM SELECTION

```
┌─────────────────────────────────────────┐
│ Czy znasz zmienną docelową?             │
├─────────────────┬───────────────────────┤
│ TAK (Supervised)│ NIE (Unsupervised)    │
└─────────────────┼───────────────────────┘
        │         │
    ┌───┴──────┐  └─────────────────┐
    │           │                     │
┌───┴────────┐ │        ┌────────────┤
│ Ciągła?    │ │        │Klasteryzacja│
├────────────┤ │        │             │
│TAK:Regresja│ │    ┌───┴──────────┬─┘
│NIE:Klasyfik│ │    │              │
└────────────┘ │ ┌──┴─────┐  ┌─────┴────┐
               │ │K-Means │  │ DBSCAN   │
        ┌──────┴─┘│Easy   │  │ Flexible │
        │   Binarna│Kuliste│  │ Shape    │
        │  Klasyfk │       │  │          │
        │          └──────┘  └──────────┘
    ┌───┴─────────────┐
    │ Dużo cech?      │
    ├─────────┬───────┤
    │TAK:SVM  │NIE    │
    │RBF      ├──┬────┤
    │NN       │  │Tree│
    │         │  │RF  │
    └─────────┴──┴────┘
```

---

**Trzymaj się tych strategii, a powinieneś radzić sobie dobrze! 🚀**
