# Ход решения
## Гипотезы
1. Существует возможность выделить кластеры, содержащие ограниченное (не сотни, а хотя бы десятки) количество культур.
2. Для каждого из таких кластеров возможно создать и обучить модель, которая предскажет, какие культуры будут засеяны на полях кластера в следующем году.
3. Список признаков можно обогатить дополнительными данными, в том числе сведениями об административном делении территории Франции, климатических зонах и т. п.
4. На части полей регулярно сеется одна и та же культура, ее предсказание тривиально.
5. Существует возможновть добиться точности (accuracy) предсказаний > 80 %.

## 1. Кластеризация
Рассматриались следующие принципы кластеризации:
1.1. Географический.<br>
1.2. На основе разреженных векторов состава засеваемых культур.<br>
1.3. На основе групп засеваемых культур.<br>
1.4. Комбинированный.

<p align="left">
  <img src="https://user-images.githubusercontent.com/11871192/111023406-f373c000-83e9-11eb-9f44-3fa3f1da8ef0.png" width="350" title="Посевы">
  <img src="https://user-images.githubusercontent.com/11871192/111023407-f4a4ed00-83e9-11eb-9dd2-ee4ce716ee7c.png" width="350" title="География">
</p>

В качестве основного был выбран принцип кластеризации на основе разреженных векторов состава засеваемых культур. При кластеризации по этому принципу было выделено большое число кластеров, содержащих одну или две культуры.

![clusters_vs_cultures](https://user-images.githubusercontent.com/11871192/111024451-e6f26600-83ef-11eb-971a-96b15e487836.png)

Географические кластеры используются как признаки при классификации.

## 2. Классификация

В качестве классификатора был выбран LightGBM - алгоритм градиентного бустинга, разработанный компанией Microsoft.<br>
Модели обучались и тестировались для каждого кластера в отдельности.<br>
Наиболее значимым признаком оказался признак географического кластера.<br>

![features](https://user-images.githubusercontent.com/11871192/111024436-d9d57700-83ef-11eb-811f-cc7d391f15ce.png)

## 3. Результаты

При обучении модели на данных за 2015-2017 годы с целью предсказания посевов на 2018 год и при валидации на тестовых данных из папки test_2019 достигнуто значение метрики **accuracy 0.8588**.<br>

При обучении модели на данных за 2015-2018 годы с целью предсказания посевов на 2019 год и при валидации на тестовых данных из папки test_2020 достигнуто значение метрики **accuracy 0.8148**.

Созданы файлы предсказаний в соответствии с поставленной задачей - **predict2019.csv** и **predict2020.csv**.

## 4. Проблемы
4.1. Время.<br>
Время на решение задачи ограничено продолжительностью хакатона. Часть гипотез не удалось проверить, так как основные этапы процесса (преимущественно сбор и обработка данных) занимают больше времени, чем отпущено.

4.2. Вычислительные мощности.<br>
Тот случай, когда данных оказалось слишком много: Google Colab падает без памяти, домашние компьютеры кипят и перезагружаются. Некоторые идеи оказалось физически невозможно реализовать из-за недостатка вычислительных мощностей, имеющихся в распоряжении команды. Некоторые по той же причине стали занимать непозволительно много времени, далее см. п. 4.1.

4.3. Компетенции.<br>
Есть вещи, которые мы хотели бы сделать, но не знаем как. Мы ведь пока еще не настоящие сварщики. Мы обязательно научимся, но это займет некоторое время, далее см. п. 4.1.

## 5. А у нас еще столько идеек было!
Краткий обзор того, что хотели бы сделать, но не смогли по причинам из раздела 4.

5.1. Кластеризация по границам департаментов (координаты -> Reverse Geocoding -> географические кластеры). Не исключено, что исторически административное деление Франции происходило, в том числе, и с учетом сельскохозяйственных соображений.<br>
5.2. Кластеризация по климатическим зонам.<br>
5.3. Кластеризация по десятилетним последовательностях групп культур с учетом цикличности.<br>
5.4. Классификация ансамблями различных алгоритмов.
