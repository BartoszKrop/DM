# DATA MINING - Notatki do Egzaminu

## Materiały przygotowawcze do zrozumienia głównych koncepcji bez skupiania się na wzorach

---

## 1. WSTĘP DO DATA MINING

### Co to jest Data Mining?
- **Cel**: Znalezienie wzorów, struktur i zależności w dużych zbiorach danych
- **Inaczej**: Wydobywanie wiedzy z danych (knowledge discovery from data)
- **Praktyka**: Od surowych danych → użyteczne informacje/predykcje

### Główne rodzaje zadań w Data Mining:

#### Uczenie nadzorowane (Supervised Learning)
- Mamy dane treningowe z już znanymi wynikami
- **Regresja**: Przewidywanie wartości ciągłych (liczby)
- **Klasyfikacja**: Przewidywanie kategorii/klas (tak/nie, A/B/C)
- Przykłady: przewidywanie ceny domu, diagnoza choroby

#### Uczenie nienadzorowane (Unsupervised Learning)
- Nie mamy znanych wyników, szukamy naturalnych grup
- **Klasteryzacja/Segmentacja**: Podział danych na grupy podobne do siebie
- Przykłady: segmentacja klientów, grupowanie dokumentów

### Etapy procesu Data Mining:
1. **Zbiór danych** → 2. **Przygotowanie danych** → 3. **Eksploracja** → 4. **Modelowanie** → 5. **Ewaluacja** → 6. **Wdrażanie**

### Jakość danych ma znaczenie!
- Brakujące wartości (missing values)
- Anomalie (outliers) - punkty bardzo różne od reszty
- Szum w danych (noise)

---

## 2. SELEKCJA ZMIENNYCH (Feature Selection)

### Dlaczego selekcja zmiennych?
- **Problem**: Mamy zbyt wiele zmiennych → zbyt skomplikowany model
- **Rozwiązanie**: Wybrać tylko najważniejsze zmienne
- **Zysk**: Szybszy model, łatwiejszy do zrozumienia, lepsze wyniki

### Główne podejścia:

#### Filter Methods (Filtrowanie)
- Oceniamy każdą zmienną **niezależnie**
- Nie patrzymy na interakcje między zmiennymi
- **Szybkie i proste**
- Przykład: Korelacja ze zmienną docelową

#### Wrapper Methods (Obudowa)
- Testujemy **kombinacje zmiennych**
- Używamy rzeczywistego modelu do oceny
- **Droższe** (trzeba uczyć wiele modeli), ale **dokładniejsze**
- Przykład: Forward selection (dodajemy zmienne jedna po jednej)

#### Embedded Methods
- Selekcja zmiennych **wbudowana w proces uczenia modelu**
- Model automatycznie dowiaduje się, które zmienne są ważne
- Przykład: Decision Trees (gałęzie dla ważnych zmiennych), Regularization

### Co szukamy?
- Zmienne **istotne statystycznie**
- Zmienne **nieskorelowane ze sobą** (aby unikać redundancji)
- Zmienne **silnie powiązane z wynikiem**

---

## 3. REGRESJA

### Idea regresji
- **Problem**: Przewidzieć wartość **ciągłą** (nie dyskretną)
- **Dane**: Rzeczywiste przykłady z wartościami docelowymi
- **Wynik**: Funkcja matematyczna, która mapuje cechy → wartość

### Regresja liniowa (Linear Regression)
- **Model**: Y = a*X + b (najprostszy przypadek)
- **Zasada**: Znaleźć linię, która najlepiej przylega do punktów
- **Kryterium**: Minimalizować błędy (różnice między przewidywaniem a rzeczywistością)
- **Kiedy używać**: Gdy relacja między zmiennymi jest liniowa
- **Zalety**: Prosty, szybki, łatwy do interpretacji
- **Wady**: Może nie wychwycić skomplikowanych relacji

### Regresja wielomianowa (Polynomial Regression)
- **Idea**: Zamiast linii, używamy krzywej (wyższych potęg zmiennych)
- **Kiedy**: Gdy relacja jest bardziej skomplikowana niż liniowa
- **Niebezpieczeństwo**: Overfitting (model zbyt dokładnie dopasowany do danych treningowych)

### Regularyzacja w regresji
- **Problem**: Model może memoryzować szum w danych
- **Rozwiązanie**: Dodać karę za zbyt skomplikowane modele
- **Ridge Regression (L2)**: Penalizuje duże współczynniki
- **Lasso Regression (L1)**: Może zerować współczynniki (selekcja zmiennych!)

### Ewaluacja regresji
- **MSE (Mean Squared Error)**: Średni kwadrat błędu - im mniejszy, tym lepiej
- **R²**: Jaki procent wariancji wyjaśniamy? (0-1, im bliżej 1, tym lepiej)
- **MAE (Mean Absolute Error)**: Średnia wartość błędu bezwzględnego

---

## 4. DRZEWA DECYZYJNE I LASY (Decision Trees & Random Forests)

### Drzewa decyzyjne
- **Idea**: Seria pytań tak/nie, które dzielą dane na coraz mniejsze grupy
- **Struktura**: Wierzchołek → gałęzie → liście (końcowe decyzje)
- **Jak budować**: Wybieramy zmienne, które **najlepiej dzielą** dane
- **Kryterium podziału**: 
  - Information Gain / Gini Index - jak dobre jest rozdzielenie klas?
  - Im większa homogeniczność grup, tym lepsze dzielenie

### Zalety drzew
- **Interpretowalne**: Możemy zobaczyć, jakie decyzje model podejmuje
- **Brak potrzeby skalowania** danych
- **Radzą sobie z relacjami nieliniowymi**
- Można użyć do **regresji i klasyfikacji**

### Wady drzew
- **Overfitting**: Drzewa mogą rosnąć zbyt głębokie i pamiętać szum
- **Instabilne**: Małe zmiany w danych mogą znacznie zmienić drzewo
- **Słabe** na niektórych danych (samo drzewo)

### Przycięcie drzewa (Pruning)
- **Cel**: Zmniejszyć rozmiar drzewa, aby lepiej uogólniało
- **Idea**: Usuwać gałęzie, które nie dają dużego polepszenia
- **Problem**: Balance między underfitting a overfitting

### Lasy losowe (Random Forests)
- **Idea**: Budujemy **wiele drzew** na losowych podzbiorach danych
- **Decyzja**: Głosowanie (klasyfikacja) lub średnia (regresja) z wszystkich drzew
- **Zaleta**: Zmniejsza wariancję i overfitting samego drzewa
- **Feature importance**: Możemy zobaczyć, które zmienne są najważniejsze

### Inne zespoły (Ensemble Methods)
- **Boosting**: Uczymy kolejne modele na błędach poprzednich (np. Gradient Boosting)
- **Bagging**: Losowe próbki z powtórzeniami, budujemy niezależne modele
- **Stacking**: Kombinujemy wiele różnych modeli

---

## 5. SIECI NEURONOWE

### Idea sieci neuronowych
- **Inspiracja**: Ludzki mózg i neurony
- **Jednostka**: Neuron - otrzymuje wejścia, oblicza, wysyła wyjście
- **Sieć**: Wiele neuronów połączonych w warstwy

### Struktura
- **Wejście (Input layer)**: Zmienne/cechy
- **Warstwy ukryte (Hidden layers)**: Neuron "myśli", łączy informacje
- **Wyjście (Output layer)**: Wynik predykcji

### Jak działa jeden neuron?
1. Otrzyma wejścia (X₁, X₂, ...) z **wagami** (W₁, W₂, ...)
2. **Suma ważona**: suma(Xᵢ * Wᵢ) + bias
3. **Funkcja aktywacyjna**: Zmienia wynik na nieliniowy (relu, sigmoid, tanh)
4. Wysyła wynik do następnej warstwy

### Ważne koncepty

#### Funkcje aktywacyjne
- **ReLU**: Zwraca max(0, x) - prosta, szybka, popularna
- **Sigmoid**: Zwraca wartość 0-1 - dobra dla klasyfikacji binarnej
- **Tanh**: Zwraca wartość -1 do 1 - zerowana średnia
- **Linear**: Nie transformuje - dla regresji

#### Warstwy
- **Gęste (Dense/Fully Connected)**: Każdy neuron połączony ze wszystkimi w poprzedniej warstwie
- **Splotowe (Convolutional - CNN)**: Dla obrazów, szuka lokalnych wzorów
- **Rekurencyjne (RNN, LSTM)**: Dla sekwencji, ma "pamięć"

#### Ucz się (Learning Process)
- **Forward pass**: Dane idą przez sieć, obliczamy wynik
- **Loss (Błąd)**: Porównujemy przewidywanie z rzeczywistością
- **Backward pass (Backpropagation)**: Błąd idzie wstecz, updatujemy wagi
- **Iteracje**: Powtarzamy, aż model się zbiegnie

### Problemy w sieciach neuronowych

#### Overfitting
- Sieć zbyt duża, memoryzuje dane treningowe
- **Rozwiązania**: 
  - Dropout - losowo "wyłączamy" neurony podczas trenowania
  - Early stopping - zatrzymujemy trenowanie, gdy wyniki na walidacji pogorszą się
  - Regularyzacja (L1, L2)

#### Vanishing/Exploding Gradients
- Gradamenty mogą być zbyt małe (zanikają) lub zbyt duże
- **Rozwiązanie**: Batch normalization, lepsze inicjalizacje

#### Hiperparametry
- Jak wiele warstw? Ile neuronów?
- Learning rate - jak szybko się uczyć?
- Batch size - po ile przykładów uczyć się za razem?
- Trzeba eksperymentować!

---

## 6. KLASTERYZACJA / SEGMENTACJA

### Co to klasteryzacja?
- **Zadanie nienadzorowane**: Nie mamy etykiet, sami szukamy grup
- **Cel**: Podzielić dane na grupy (klastry) takie, że:
  - Dane w tej samej grupie są **podobne do siebie**
  - Dane z różnych grup są **różne od siebie**

### K-Means (najpopularniejszy algorytm)
- **Idea**: Znaleźć K centrów klastrów i przypisać każdy punkt do najbliższego
- **Jak działa**:
  1. Losowo wybierz K środków (centrów)
  2. Przypisz każdy punkt do najbliższego środka
  3. Przesunąć środek do średniej punktów w klastrze
  4. Powtarzaj kroki 2-3, aż się nie zmienia
- **K - ile klastrów?**: Trzeba wybrać! (Elbow method, Silhouette score)
- **Zalety**: Prosty, szybki, intuicyjny
- **Wady**: Musi być kuliste klastry, wrażliwy na inicjalizację

### Hierarchical Clustering
- **Idea**: Budować drzewo klastrów (dendrogram)
- **Top-down (Divisive)**: Zaczynamy z jednym klastrem, dzielimy
- **Bottom-up (Agglomerative)**: Zaczynamy z każdym punktem oddzielnie, łączymy
- **Jak łączyć**: 
  - Single linkage: Najmniejsza odległość między dowolnymi dwoma punktami
  - Complete linkage: Największa odległość
  - Average linkage: Średnia odległość
- **Zaleta**: Dendrogram pokazuje naturalną hierarchię
- **Wada**: Drożej obliczeniowo, może być ciężko zdecydować gdzie "przeciąć"

### DBSCAN
- **Idea**: Klastry to gęste regiony, szum to izolowane punkty
- **Jak**: Szukamy punktów bliskich sobie i łączymy je
- **Parametry**: 
  - eps: jaka odległość to "bliskie"?
  - min_points: ile punktów w sąsiedztwie, aby być rdzeniem?
- **Zaleta**: Może znaleźć klastry dowolnego kształtu!
- **Wada**: Trzeba dobrać parametry, wrażliwy na gęstość

### Ewaluacja klasteryzacji
- **Silhouette score**: -1 do 1, im wyżej tym lepiej (czy punkt jest bliżej swojego klastra niż innych?)
- **Davies-Bouldin Index**: Im niżej tym lepiej (mierzy separację klastrów)
- **Inertia**: Suma odległości punktów do ich centrów (dla K-Means)
- **Elbow method**: Patrzymy na wykres, szukamy "łokcia" gdzie zmiana przestaje być znacząca

---

## 7. SUPPORT VECTOR MACHINES (SVM)

### Główna idea
- **Cel**: Znaleźć **linię/hiperpłaszczyznę**, która dzieli dane na klasy
- **Optymalizacja**: Linia powinna być jak najdalej od obu klas (maksymalizujemy margines)
- **Intuicja**: Im szerszy margines, tym lepiej generalizuje

### Liniowe SVM (Linear SVM)
- **Dane**: Separowalne - można je rozdzielić linią
- **Wynik**: Linia decyzji (decision boundary)
- **Support vectors**: Punkty najbliżej linii - to są "ważne" punkty

### Nieliniowe SVM - Kernel Trick
- **Problem**: Co gdy dane nie są liniowo separowalne?
- **Rozwiązanie**: Transformować dane do wyższej liczby wymiarów, gdzie są separowalne!
- **Trick**: Nie musimy eksplicitnie transformować - używamy funkcji kernela

#### Popularne kernele
- **Linear**: Dla danych liniowo separowalnych
- **Polynomial**: Transformacja wielomianowa - czasem przydatna
- **RBF (Radial Basis Function)**: Najczęściej używany! Bardzo elastyczny
- **Sigmoid**: Mniej popularne

### Parametry SVM

#### C (Cost/Regularization)
- **Duże C**: Model bardziej dopasowany do danych treningowych, wyższe overfitting
- **Małe C**: Bardziej tolerancyjny, może underfitting
- **Balans**: Trzeba znaleźć!

#### Gamma (dla kernela RBF)
- **Duża gamma**: Każdy punkt treningowy ma lokalny wpływ (overfitting)
- **Mała gamma**: Szerszy wpływ (underfitting)

### Zalety i wady

**Zalety**:
- Bardzo efektywny dla klasyfikacji binarnej
- Działa dobrze w wysokiej liczbie wymiarów
- Kernel trick pozwala na elastyczne modele

**Wady**:
- Trudne do interpretacji (black box)
- Klasyfikacja wieloklasowa trzeba robić "po dwa" (one-vs-rest)
- Drożej obliczeniowo dla dużych zbiorów danych

---

## 8. PRZEFITTING vs NIEDOFITTING (Overfitting vs Underfitting)

### Underfitting
- **Problem**: Model zbyt prosty, nie uczy się wzorów w danych
- **Symptomy**: Słabe wyniki na danych treningowych i testowych
- **Rozwiązanie**: Bardziej skomplikowany model, więcej cech, uczenie dłużej

### Overfitting
- **Problem**: Model zbyt skomplikowany, memoryzuje szczegóły i szum
- **Symptomy**: Doskonałe wyniki na treningowych, słabe na testowych
- **Rozwiązanie**: Prostszy model, mniej cech, regularyzacja, więcej danych

### Cross-validation
- **Idea**: Podzielić dane na kilka części, uczyć na niektórych, testować na innych
- **K-fold**: Podziel na K części, powtórz K razy (różne części jako test)
- **Cel**: Uniknąć nadmiernego dopasowania do jednego podziału

---

## 9. METRYKI EWALUACJI

### Dla Klasyfikacji Binarnej

#### Confusion Matrix (Macierz błędów)
```
                Przewidywany: TAK    TAK: NIE
Rzeczywisty TAK      TP              FN
Rzeczywisty NIE      FP              TN
```

- **TP (True Positive)**: Dobrze przewidzieliśmy TAK
- **FP (False Positive)**: Błędnie przewidzieliśmy TAK (Type I error)
- **FN (False Negative)**: Błędnie przewidzieliśmy NIE (Type II error)
- **TN (True Negative)**: Dobrze przewidzieliśmy NIE

#### Ważne metryki
- **Accuracy**: (TP + TN) / wszystkie = czy na ogół mamy rację?
- **Precision**: TP / (TP + FP) = z naszych pozytywnych, ile było faktycznie pozytywnych?
  - Ważna gdy False Positives są kosztowne
- **Recall (Sensitivity)**: TP / (TP + FN) = z faktycznych pozytywnych, ile złapaliśmy?
  - Ważna gdy False Negatives są kosztowne (np. choroby)
- **F1 Score**: Średnia harmoniczna Precision i Recall
- **Specificity**: TN / (TN + FP) = ile dobrze zidentyfikowaliśmy negatywów?

#### ROC Curve
- X-axis: False Positive Rate (FPR)
- Y-axis: True Positive Rate (TPR)
- **AUC (Area Under Curve)**: 0-1, im wyżej tym lepiej
- Pokazuje trade-off między TP a FP

### Dla Regresji
- **MAE**: Średnia wartość absolutna błędu
- **MSE**: Średni kwadrat błędu (penalizuje duże błędy bardziej)
- **RMSE**: Pierwiastek MSE - w tej samej skali co wynik
- **R²**: Jaki procent wariancji wyjaśniamy? (0-1)

---

## 10. STANDARYZACJA I NORMALIZACJA

### Dlaczego?
- Różne zmienne mogą mieć różne skale (np. wiek: 18-100 vs zarobki: 1000-100000)
- Niektóre algorytmy (KNN, SVM, sieci neuronowe) wrażliwe na skalę

### Standardization (Z-score normalization)
- Centra dane wokół 0, skaluj do ~1
- Formula: (X - mean) / standard_deviation
- Wynik: ~95% danych między -2 a 2

### Normalization (Min-Max scaling)
- Skaluj do zakresu [0, 1] lub [-1, 1]
- Formula: (X - min) / (max - min)
- Wynik: Wszystkie wartości między 0 a 1

### Kiedy używać?
- **Zawsze dla**: KNN, SVM, Neural Networks, K-Means
- **Opcjonalnie dla**: Decision Trees (nie wrażliwe na skalę!)

---

## 11. IMBALANCED DATA (Niezbalansowane dane)

### Problem
- Klasy nie są równomiernie rozpodzielone (np. 95% negatywów, 5% pozytywów)
- Model może być zbyt chętny do przewidywania klasy większościowej

### Rozwiązania
- **Upsampling**: Powielanie przykładów z klasy mniejszościowej
- **Downsampling**: Usuwanie przykładów z klasy większościowej
- **SMOTE**: Syntetyczne generowanie nowych przykładów
- **Class weights**: Powiedzieć modelowi, że jedna klasa jest ważniejsza
- **Different metrics**: Używać F1 zamiast Accuracy

---

## 12. HYPER-PARAMETER TUNING

### Manualne
- Eksperymentować z różnymi wartościami
- Obserwować wyniki

### Grid Search
- Spróbuj wszystkie kombinacje parametrów
- Czasochłonne, ale dokładne

### Random Search
- Spróbuj losowe kombinacje
- Szybsze, czasem lepsze wyniki

### Bayesian Optimization
- Inteligentne wyszukiwanie - uczy się, które wartości są obiecujące
- Najtańsze obliczeniowo dla dużych space'ów

---

## 13. ENSEMBLE METHODS - PODSUMOWANIE

### Dlaczego zespoły?
- Wiele słabych modeli → jeden silny model
- Zmniejsza variance i bias

### Główne podejścia

**Parallel Ensembles** (Modele niezależnie):
- Bagging, Random Forests
- Zmniejsza variance

**Sequential Ensembles** (Modele uczą się na błędach poprzednich):
- Boosting, Gradient Boosting
- Zmniejsza bias

**Hybrid**:
- Stacking - trenujemy meta-model na predykcjach bazowych modeli
- Blending

---

## 14. TYP PYTAŃ EGZAMINACYJNYCH - CO ZWYKLE SIĘ POJAWIA?

### Pytania koncepcyjne
❓ Co to jest Data Mining?
❓ Różnica między supervised a unsupervised learning?
❓ Kiedy użyć regresji a kiedy klasyfikacji?
❓ Overfitting - co to jest i jak go unikać?
❓ Jakie są różnice między K-Means a Hierarchical Clustering?

### Pytania analityczne
❓ Dany zbiór danych - czy powinniśmy użyć SVM czy Neural Network?
❓ Problem z czymś w przefitowaniu - jak to naprawić?
❓ Metryka A vs B - która lepsza dla danego scenariusza?
❓ Jak byś podszedł do problemu X?

### Pytania praktyczne
❓ Jak będziesz wybierać zmienne?
❓ Jak budujesz i ewaluujesz model?
❓ Jak interpretujesz wyniki?
❓ Jakie są zagrożenia w podejściu Y?

### Pytania o interpretacje
❓ Kiedy preferujesz prosty model a kiedy skomplikowany?
❓ Trade-off między dokładnością a interpretowalności?
❓ Jak komunikujesz wyniki biznesowe?

---

## 15. PRAKTYCZNE WSKAZÓWKI NA EGZAMINIE

### Jeśli dostajesz problem:

1. **Zrozum problem**
   - Co chcemy przewidzieć? (ktoś da ci zbiór)
   - Kolumna docelowa jest znana? (supervised czy unsupervised?)
   - Jak duży zbiór danych?

2. **Wybierz typ zadania**
   - Zmienna docelowa ciągła? → Regresja
   - Zmienna docelowa kategoryczna? → Klasyfikacja
   - Brak zmiennej docelowej? → Klasteryzacja

3. **Zaproponuj algorytm**
   - Jaki jest kształt danych? (liniowy? skomplikowany?)
   - Potrzebujesz interpretacji czy dokładności?
   - Ile danych masz?

4. **Dyskutuj preprocesing**
   - Standaryzacja/Normalizacja
   - Brakujące wartości
   - Outliers
   - Selekcja zmiennych

5. **Metryki**
   - Jaka metryka dla tego problemu?
   - Czemu ta metryka, a nie inna?
   - Cross-validation!

### Cześć części, których chyba będzie
- Porównanie algorytmów
- Interpretacja drzewa/modelu
- Dyskusja o overfitting
- Selekcja zmiennych
- Ewaluacja modelu
- Praktyczne decyzje (co zrobić gdy X?)

---

## PODSUMOWANIE - CZEAT SHEET

| Zadanie | Algorytm | Kiedy | Zaleta | Wada |
|---------|----------|-------|--------|------|
| **Regresja (liniowa)** | Linear Regression | Relacja liniowa | Prosty, szybki | Ograniczona |
| **Regresja (skomplikowana)** | Polynomial/Tree | Wzory złożone | Elastyczny | Overfitting |
| **Klasyfikacja (binarnym)** | Logistic Regression/SVM | Klasyczne | Interpretowalne | Może być słabe |
| **Klasyfikacja (multi-class)** | Decision Tree/Random Forest/NN | Średnia złożoność | Efektywne | Черный ящик |
| **Klasteryzacja** | K-Means | Szybkie | Proste | Kuliste klastry |
| **Klasteryzacja (dowolny kształt)** | DBSCAN | Kompleksowe | Elastyczne | Parametry trudne |
| **High-dimensional** | SVM z RBF | Dużo zmiennych | Efektywne | Drożej |
| **Interpretacja** | Tree/Rules | Działalność biznesu | Przejrzyste | Może być słabe |
| **Maksymalna dokładność** | Ensemble/NN | Konkurencja | Dokładne | Czarny pudełek |

---

## OSTATNIE SŁOWA

✅ **Pamiętaj**:
- Nie musisz znać dokładnych wzorów!
- Pamiętaj **ideę** i **kiedy używać** każdego algorytmu
- **Trade-off'y**: Prostota vs Dokładność, Bias vs Variance, Underfitting vs Overfitting
- **Proces ważniejszy niż wynik**: Jak podchodziłeś do problemu?
- **Justyfikacja**: Dlaczego wybrałeś ten algorytm, tę metrykę?

**Powodzenia na egzaminie! 🚀**
