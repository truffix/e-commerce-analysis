# e-commerce-analysis
### Цель
Выполнить анализ данных заказов электронного магазина, а именно Ad-hoc анализ, выявить когорту с самым высоким retention на 3й месяц и провести RFM сегментацию.
### Стэк
pandas, requests, matplotlib, plotly, sklearn
### Выполненные задачи
1. Выгружены данные с Яндекс Диска.  
   Данные представляю собой несколько отдельных таблиц в формате csv (Пользователи, Товары, Заказы) и хранятся на Яндекс Диске. 
   С помощью библиотеки requests и Яндекс API реализована загрузка датафреймов при передаче списка ссылок и их автоматическое наименование на основании имен файлов.
2. Обработка данных и общая характеристика.
   - Все колонки времени приведены к единому формату.
   - Наибольшее кол-во заказов имеют статус 'delivered', наименьшее - 'approved'  
     ![order_stat](https://raw.githubusercontent.com/truffix/e-commerce-analysis/main/pic/order_stat.png)
   - Данные представлены за 2 года  
     ![time](https://raw.githubusercontent.com/truffix/e-commerce-analysis/main/pic/time.png)
4. Выполнен Ad-hoc анализ для ответа на такие вопросы как  
   - Кол-во пользователей, которые совершили покупку только один раз  
     91814, что равно 97% всех пользователей

   - Заказов в месяц в среднем не доставляется по разным причинам
   
   | order_status | mean_orders_per_month |
   |-------------:|-----------------------|
   |     canceled |                 26.04 |
   |  unavailable |                 29.00 |  
     
   - По каждому товару определить, в какой день недели товар чаще всего покупается
   
   |       |                       product_id | purches_dow | quantity |
   |------:|---------------------------------:|------------:|----------|
   | 15898 | 422879e10f46682990de24d770e7f83d |   Wednesday |       93 |
   | 36512 | 99a4788cb24856965c36a24e339b6058 |      Monday |       92 |
   | 41044 | aca2eb7d00ea1a7b8ebd4e68314663af |    Thursday |       89 |
   | 20123 | 53b36df67ebb7c41585e8d54d6772e08 |     Tuesday |       76 |
   | 13536 | 389d119b48cf3043d311335e499d9c6b |    Thursday |       67 |
   |   ... |                              ... |         ... |      ... |

   - Сколько у каждого из пользователей в среднем покупок в неделю (по месяцам)
   
   |               customer_unique_id | purches_month | mean_quantity_of_orders_per_month |
   |---------------------------------:|--------------:|----------------------------------:|
   | 0000366f3b9a7992bf8c76cfdf3221e2 |             5 |                               1.0 |
   | 0000b849f77a49e4a4ce2b2a4ca5be3f |             5 |                               1.0 |
   | 0000f46a3911fa3c0805444483337064 |             3 |                               1.0 |
   | 0000f6ccb0745a6a4b88665a16c9f078 |            10 |                               1.0 |
   | 0004aac84e0df4da2b147fca70cf8255 |            11 |                               1.0 |
   |                              ... |           ... |                               ... |

   
6. Когортный анализ пользователей
   - Выполнил разделение на когорты по месяцам
   - Рассчитал месячный retention для каждой когорты
   - Оформил в виде хитмап для наглядности
   - Расчет был выполнен в двух вариантах для кросс чека

   |  cohort | size of cohort | mean_quantity_of_orders_per_month |
   |--------:|---------------:|----------------------------------:|
   | 2017-06 |      3139      |                0.41               |
   | 2017-05 |      3596      |                0.39               |
   | 2017-03 |      2636      |                0.38               |
   | 2017-12 |      5487      |                0.35               |
   | 2017-09 |      4130      |                0.29               |
   | 2017-08 |      4184      |                0.26               |
   | 2017-07 |      3894      |                0.26               |
   | 2017-11 |      7304      |                0.18               |
   | 2017-04 |      2352      |                0.17               |
   | 2017-01 |       764      |                0.13               |
   | 2017-02 |      1752      |                0.11               |
   | 2017-10 |      4470      |                0.09               |
     
8. RFM сегментация пользователей
   Выполнил сегментацию пользователей по квантилям с использованием метрик Recency,	Frequency,	Monetary по стандартной семантике.  
   В результате выявлено, что подавляющее кол-во пользователей относятся к группе "Спящих". Магазину требуется повести мероприятия для увеличения активности пользователей: разработка РК, промоакции, улучшение системы предложений и т.д.  
   Кроме этого, приведен вариант разделения пользователей с помощью метода k-средних.
   
