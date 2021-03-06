# Ментальное здоровье
Прогнозирование ментальных проблем у работников IT-сферы

## I этап: Изучение данных

Данные были взяли с Kaggle (https://www.kaggle.com/osmi/mental-health-in-tech-survey). Опрос людей проводился в 2014 году и всего было опрошено 1259 человек по 27 вопросами, связанными с работой и ментальным здоровьем сотрудника. По официально зарегистрированным случаям наличия заболеваний выборка получилась сбалансированной: 637 имеют болезни, связанные с психическим здоровьем и 622 официально не имеют таких проблем. Важно отметить, что данные были собраны со всего мира, но в выборке значительно преобладают жители Соединенных Штатов и Великобритании.

## II этап: Преобразование переменных

Многие из значений переменных были закодированы в форматы ответов "Да/Нет" или "Никогда/Редко/Часто". С помощью библиотеки pandas все они перекодированы в числовой формат и стали категориальными. Для переменой "Гендер" были применены One-Hot Encoding, то есть добавились еще три колонки: Male, Female and Non-binary. 
Все значения NaN были заменены средними или самыми популярными значениями.

Выборка была поделена на train и valid в соотношении 80/20. Данные были пронормированы с помощью Standard Scaler для приведения их к одному масштабу. 

## III этап: Обучение  

Для обучения были испробованы следующие методы машинного обучения: логистическая регрессия, метод ближайших соседей, метод опорных векторов, дерево решений совместно с Grid Search и Cross-Validation, рандомный лес (GS + CV) и XGBoost (GS + CV). Результаты обучения моделей оценивались по метрике recall, которая включает в себя ошибку 2 рода. Эта метрика хорошо подходит для поставленной задачи, так как в случае с ментальным здоровьем лучше ошибочно поставить человеку диагноз, когда его на самом деле нет, чем, наоборот, пропустить болезнь и человека с заболеванием, не диагностировав у него проблемы психологического характера. Полученные результаты для валидационной выборки можно посмотреть в таблице: 

| № | Model                 | Recall  |
| --|:---------------------:| -------:|
| 1 | XGBClassifier         | 92.3100 |
| 2 | DecisionTreeClassifier| 87.6900 |
| 3 | RandomForestClassifier| 87.6900 |
| 4 | KNN                   | 80.0000 |
| 5 | SVM                   | 78.2258 |
| 6 | Logistic Regression   | 77.7800 |


## IV этап: Feature 

Данный опросник можно применять для компаний в IT-сфере для диагностики и отслеживания ментального состояния своих сотрудников. В случае положительных результатов поддерживать и вовремя предоставлять квалифицированную помощь своим работникам.
