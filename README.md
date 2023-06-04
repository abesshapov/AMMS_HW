# AMMS_HW
Домашнее задание по дисциплине "Прикладные методы математической статистики"
## Вариант 4

Выполнили студенты группы БПИ219 Бесшапов Алексей, Жуковский Дмитрий, Швецов Данил.

## Препроцессинг данных

Данные в таблице были изменены следующим образом:
- Столбец rules_viol: 1, если количество нарушений правил в тюрьме больше "1.23" (среднее по таблице), 0 в ином случае.
- Столбец age_aaa: 1, если возраст в месяцах больше "342.3" (среднее по таблице), 0 в ином случае.

## Начало работы

Были выбраны следующие переменные:
- Объясняемая переменная: recid.
- Регрессоры: age_aaa, black, married, alcohol, rules_viol.

## Задание 16

Ниже приведены оценки моделей:

- линейная модель:

![image](https://github.com/abesshapov/AMMS_HW/assets/45789410/66d0b168-f011-442c-93a7-4b57b94d9c36)

- логит:

![image](https://github.com/abesshapov/AMMS_HW/assets/45789410/352f3eb7-0db5-42ce-aecf-bcd4477b6d03)

- пробит:

![image](https://github.com/abesshapov/AMMS_HW/assets/45789410/2f2edbce-4eef-4884-b614-7109ecf49227)

## Задание 17

Результаты оценки модели логит:

- переменная age_aaa значима на уровне 6.9% и выше;
- переменная black значима на уровне 0.01% и выше;
- переменная married значима на уровне 12.7% и выше;
- переменная alcohol значима на уровне 0.11% и выше;
- переменная rules_viol значима на уровне 0.000111% и выше;
- ковариационная матрица оценок коэффициентов:

![image](https://github.com/abesshapov/AMMS_HW/assets/45789410/e83511f2-4700-44a3-98ce-101e6732a0ae)

Выводы из оценки: оценки коэффициентов показывают, что:
- нарушения правил в тюрьме, проблемы с алкоголем, принадлежность к негроидной расе - факторы, повышающие вероятность повторного совершения преступлений;
- женатость, возраст более 28 лет - факторы, понижающие вероятность повторного совершения преступлений. 

## Задание 18

На основе полученных оценок были оценены вероятности повторного преступления для всех наблюдений для трех моделей. 

Между прогнозами наблюдались незначительные различия, например:
- наибольшее различие в прогнозе между линейной моделью и логит моделью: 0.017, наблюдение номер 7;
- наибольшее различие в прогнозе между линейной моделью и пробит моделью: 0.014, наблюдение номер 7;
- наибольшее различие в прогнозе между моделями логит и пробит: 0.003, наблюдение номер 33.

Для каждой модели были определены преступники, еще не совершившие рецидив, которым следует уделить особое внимание. Для этого среди данных наблюдений (965-1014) были найдены те, для которых вероятность больше 0.5:
- для линейной модели (номер наблюдения, вероятность): (966, 0.552107), (968, 0.544559), (975, 0.606512), (982, 0.606512), (988, 0.606512);
- для логит модели (номер наблюдения, вероятность): (966, 0.553184), (968, 0.545976), (975, 0.613001), (982, 0.613001), (988, 0.613001);
- для пробит модели (номер наблюдения, вероятность): (966, 0.551436), (968, 0.54747), (975, 0.61143), (982, 0.61143), (988, 0.61143).

Все модели указывают на набор из пяти наблюдений, следовательно, данным бывшим заключенным требуется уделить внимание, так как для них высока вероятность рецидива.

## Задание 19

Проверим значимость пробит модели тестом отношения правдоподобия. Выдвигается гипотеза, что все коэффициенты, за исключением константы, равны "0".  

Для модели без ограничений значение логарифмической функции правдоподобия:

![image](https://github.com/abesshapov/AMMS_HW/assets/45789410/8c2e495b-f342-4c12-b3e6-260edaaee15b)

Для модели с ограничениями:

![image](https://github.com/abesshapov/AMMS_HW/assets/45789410/cfc4d0e3-ac03-4388-9f1d-b68fe2a2c966)

Тогда LR = 52.8978, имеет асимптотическое распределение с пятью степенями свободы. Значение функции chi2cdf: 1, p-value = 0. Следовательно, гипотеза о незначимости регрессии в целом отвергается на любом уровне значимости.

## Задание 20

Данное задание выполнено для пробит модели. Требуется определить чувствительность и специфичность модели для различных пороговых значений с от "0" до "1" с шагом "0.05". Были получены следующие графики:

- зависимость чувствительности от порогового значения:

![image](https://github.com/abesshapov/AMMS_HW/assets/45789410/9da009fe-569b-4931-87c7-c13c5da9a4ea)

- зависимость специфичности от порогового значения:

![image](https://github.com/abesshapov/AMMS_HW/assets/45789410/a66e5a4f-f186-4a52-8a3a-279254faba49)

Требуется, чтобы чувствительность прогнозной модели была не ниже 80%. Пороговые значения, при которых это достигается:
- c = 0.0, чувствительность 1, специфичность 0;
- c = 0.05, чувствительность 1.0, специфичность 0.0;
- c = 0.1, чувствительность 1.0, специфичность 0.0;
- c = 0.15, чувствительность 1.0, специфичность 0.0;
- c = 0.2, чувствительность 1.0, специфичность 0.0;
- c = 0.25, чувствительность 0.937, специфичность 0.108;
- с = 0.3, чувствительность 0.924, специфичность 0.175.
