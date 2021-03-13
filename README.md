# Ход решения
## Гипотезы
1. Существует возможность выделить кластеры, содержащие ограниченное (не сотни, а хотя бы десятки) количество культур.
2. Для каждого из таких кластеров возможно создать и обучить модель, которая предскажет, какие культуры будут засеяны на полях кластера в следующем году.
3. Существует возможновть добиться точности (accuracy) предсказаний > 80 %.

## 1. Кластеризация
Рассматриались следующие принципы кластеризации:
1.1. Географический.
1.2. На основе разреженных векторов состава засеваемых культур.
1.3. На основе групп засеваемых культур.
1.4. Комбинированный.

<p align="left">
  <img src="https://user-images.githubusercontent.com/11871192/111023406-f373c000-83e9-11eb-9f44-3fa3f1da8ef0.png" width="350" title="Посевы">
  <img src="https://user-images.githubusercontent.com/11871192/111023407-f4a4ed00-83e9-11eb-9dd2-ee4ce716ee7c.png" width="350" title="География">
</p>

## 2. Классификация

В качестве основного был выбран принцип кластеризации на основе разреженных векторов состава засеваемых культур. При кластеризации по этому принципу было выделено большое число кластеров, содержащих одну или две культуры.

Географические кластеры используются как признаки при кластеризации.

В качестве классификатора был выбран LightGBM - алгоритм градиентного бустинга, разработанный компанией Microsoft.

## 3. Результаты

При обучении модели на данных за 2015-2017 годы с целью предсказания посевов на 2018 год и при валидации на тестовых данных из папки test_2019 достигнуто значение метрики accuracy 0.8588.

При обучении модели на данных за 2015-2018 годы с целью предсказания посевов на 2019 год и при валидации на тестовых данных из папки test_2020 достигнуто значение метрики accuracy 0.8148.
