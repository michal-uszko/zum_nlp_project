# Analiza sentymentu
## Korzystanie z plików
Projekt składa się głównie z notebooka pythonowego NLP_praca_domowa.ipynb. Do korzystania z notebooka
nie potrzeba żadnych zewnętrznych plików, dane pobierane są z poziomu notebooka. Należy jedynie samemu
zainstalować użyte w notebooku biblioteki. Dodatkowo, zamieszczono również pliki z wytrenowanymi modeli, aby nie trzeba było trenować ich od zero, co może być czasochłonne.


## Cel projektu
Celem projektu było zastosowanie różnych metod do przeprowadzenia analizy sentymentu na własnych danych. Do osiągnięcia tego celu zastosowano 4 metody:
- Trening na modelu sieci rekurencyjnej **GRU**
- Trening na modelu sieci **CNN**
- Trening z wykorzystaniem z pre-trenowanych word embeddingów, w tym przypadku użyto globalnych wektorów **GloVE** (w tym przypadku również zastosowano model GRU)
- Fine-tuning modelu językowego, w tym przypadku wykorzystano **GPT2**

## Dane
Dane wykorzystane w projekcie zawierają recenzje gier użytkowników platformy Steam. Każda recenzja posiada flagę określającą, czy recenzja była pozytywna bądź negatywna. Analiza sentymentu dla tych danych polega więc na tym, aby na podstawie treści tekstu określić, czy ma on sentyment pozytywny
czy negatywny. Recenzje są w języku angielskim.

## Model GRU

W projekcie zastosowano model sieci rekurencyjnej GRU (Gated Recurrent Unit) do analizy sentymentu na danych tekstowych. Model GRU jest jednym z rodzajów rekurencyjnych sieci neuronowych, który jest szczególnie efektywny w przetwarzaniu sekwencji danych.

### Architektura modelu

Model GRU składa się z warstw embeddingu, warstwy GRU i warstwy wyjściowej. Warstwa embeddingu przekształca słowa na wektory liczbowe, które są wejściem dla warstwy GRU. Warstwa GRU przetwarza sekwencję wektorów i generuje ukryte stany dla każdego kroku czasowego. Na podstawie ukrytych stanów, warstwa wyjściowa przewiduje sentyment jako wartość wyjściową.

### Trening modelu

Model GRU jest trenowany na danych treningowych, które zawierają recenzje gier wraz z ich sentymentem. Podczas treningu, model jest optymalizowany w celu minimalizacji funkcji straty, tak aby jak najlepiej przewidywał sentyment na danych testowych.

### Zalety modelu GRU

Model GRU ma kilka zalet, które sprawiają, że jest popularny w analizie sentymentu:
- Efektywne przetwarzanie sekwencji danych
- Możliwość uwzględnienia kontekstu w analizie sentymentu
- Skuteczność w rozpoznawaniu zależności między słowami w tekście

