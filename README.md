# Analiza sentymentu
## Korzystanie z plików
Projekt składa się głównie z notebooka pythonowego NLP_praca_domowa.ipynb. Do korzystania z notebooka
nie potrzeba żadnych zewnętrznych plików, dane pobierane są z poziomu notebooka. Należy jedynie samemu
zainstalować użyte w notebooku biblioteki.   

Dodatkowo, zamieszczono również pliki z wytrenowanymi modelami, aby nie trzeba było trenować ich od zera, co może być czasochłonne (folder **models**). Wyjątkiem jest model GPT2, który jest zbyt duży, aby umieścić go w zdalnym repozytorium.  

Przetworzone dane wejściowe są zapisywane do pliku *steam_reviews_clean.csv* po ich pre-processingu, aby nie trzeba było powtarzać procesu za każdym razem (sama lemmatyzacja trwa ok. 30 min.). Proces zapisu znajduje się tuż przed sekcją "Wczytanie danych z 
pliku" w notebooku.


## Cel projektu
Celem projektu było zastosowanie różnych metod do przeprowadzenia analizy sentymentu na własnych danych. Do osiągnięcia tego celu zastosowano 4 metody:
- Trening na modelu sieci rekurencyjnej **GRU**
- Trening na modelu sieci **CNN**
- Trening z wykorzystaniem z pre-trenowanych word embeddingów, w tym przypadku użyto globalnych wektorów **GloVE** (w tym przypadku również zastosowano model GRU)
- Fine-tuning modelu językowego, w tym przypadku wykorzystano **GPT2**

## Dane
Dane wykorzystane w projekcie zawierają recenzje gier użytkowników platformy Steam. Każda recenzja posiada flagę określającą, czy recenzja była pozytywna bądź negatywna. Analiza sentymentu dla tych danych polega więc na tym, aby na podstawie treści tekstu określić, czy ma on sentyment pozytywny
czy negatywny. Recenzje są w języku angielskim.

link: https://www.kaggle.com/datasets/andrewmvd/steam-reviews

Kolumny w zbiorze:
- **app_id** - identyfikator gry
- **app_name** - nazwa gry
- **review_text** - treści recenzji
- **review_score** - sentyment recenzji (pozytywny lub negatywny)
- **review_votes** - oznaczenie, czy dana recenzja została uznana przez innych użytkowników za przydatną (1)
czy też nie (0)

Zbiór składa się z ponad 6,4mln rekordów. W trenowaniu modeli wykorzystano **review_score** (label) i **review_text** (feature), zaś **review_votes** posłużyło do wybrania tylko przydatnych recenzji.

## Model GRU

W projekcie zastosowano model sieci rekurencyjnej GRU (Gated Recurrent Unit) do analizy sentymentu na danych tekstowych. Model GRU jest jednym z rodzajów rekurencyjnych sieci neuronowych, który jest szczególnie efektywny w przetwarzaniu sekwencji danych.

### Architektura modelu

Model GRU składa się z warstw embeddingu, warstwy GRU i warstwy wyjściowej. Warstwa embeddingu przekształca słowa na wektory liczbowe, które są wejściem dla warstwy GRU. Warstwa GRU przetwarza sekwencję wektorów i generuje ukryte stany dla każdego kroku. Na podstawie ukrytych stanów, warstwa wyjściowa przewiduje sentyment jako wartość wyjściową.

### Trening modelu

Model GRU jest trenowany na danych treningowych, które zawierają recenzje gier wraz z ich sentymentem. Podczas treningu, model jest optymalizowany w celu minimalizacji funkcji straty, tak aby jak najlepiej przewidywał sentyment na danych testowych.

### Zalety modelu GRU

Model GRU ma kilka zalet, które sprawiają, że jest popularny w analizie sentymentu:
- Efektywne przetwarzanie sekwencji danych
- Możliwość uwzględnienia kontekstu w analizie sentymentu
- Skuteczność w rozpoznawaniu zależności między słowami w tekście

