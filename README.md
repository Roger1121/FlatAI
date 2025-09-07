# FlatAI
Projekt miał za zadanie opracowanie modelu do predykcji cen mieszkań w oparciu o archiwalne dane  serwisów ogłoszeniowych. Zbiór danych użyty do treningu modeli pochodził z okresu 08.2023-10.2023. Oprócz cech mieszkań (powierzchnia, piętro, cena… ) zawiera również informacje o punktach zainteresowań w okolicy oraz informacje o budynkach, w których się znajdują. 

## Przygotowanie danych

### Usunięcie wybranych cech
W pierwszym etapie weryfikacji dane zostały oczyszczone poprzez usunięcie cech o najwyższym odsetku braków (buildingMaterial, condition, type) oraz cechy wysoko skorelowane ze sobą nawzajem (odległości odszkół, klinik, przedszkoli itp. - reprezentowane są rownież przez kolumnę przedstawiającą liczbę punktów zainteresowania w okolicy).

### Uzupełneinie braków
Braki w atrybutach buildYear, floorCount oraz floor wypełniono medianami wartości z kolumny. W przypadku cechy hasElevator przyjęto, że każdy budynek o wysokości powyżej 4 pięter posiada windę, natomiast pozostałe nie (dotyczy tylko, gdy brak danych)

### Zmiany w reprezentacji
Atrybut city zakodowano metodą one-hot.

## Podstawowy model

Pierwszym przetestowanym algorytmem była sieć neuronowa DNN. Przetestowaliśmy trening sieci przez 100 i 200 epok oraz dodatkowe wersje działające na danych po usunięciu najmniej istotnych kolumn (100 i 200 epok), usunięciu danych odstających (100 epok) oraz po zastosowaniu dropoutu (200 epok). W najlepszym scenariuszu (model podstawowy trenowany przez 200 epok) udało nam się uzyskać predykcje ceny ze średnią dokładnością wynoszącą 8,4% różnicy (czyli ok. 55 tys zł różnicy między rzeczywistą ceną, a predykcją sieci).

## Inne modele

W ramach projektu przetestowaliśmy również inne modele:
 - Kernel Ridge Regression - średnio uzyskaliśmy błąd na poziomie 12,2%, model najgorzej radził sobie z mieszkaniami o wysokiej wartości
 - Decision Trees Regression - ten model uzyskał najwyższą skuteczność ze średnim błędem na poziomie 5,8%. Okazał się on być również najmniej wymagający obliczeniowo
 - Nearest Neighbors Regression - średni błąd dla tego modelu wyniósł 11%
