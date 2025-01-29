## Данные о доходах компании Netflix

Для создания датасета использовались таблицы `CONSOLIDATED STATEMENTS OF OPERATIONS` из официальных отчетов Netflix.

Структура этих таблиц менялась, поэтому в итоговой таблице есть пропущенные значения (часть информации из ранних таблиц не добавлена, часть столбцов вероятно можно объединить, если использовать знания экспертов).

С 2012 по 2023 год данные почти полные для выбранных столбцов.

Значения приводятся в тысячах долларов, за исключением значений на акцию (per share).

Структура таблицы из отчета и связь с датасетом:

|                                             | Название столбца в таблице отчета   |                            | название колонки                  | единицы измерения | не пропущенные значения с 2002 по 2023 | не пропущенные значения с 2012 по 2023 |
| ------------------------------------------- | ----------------------------------- | -------------------------- | --------------------------------- | ----------------- | -------------------------------------- | -------------------------------------- |
| Revenues:                                   |                                     |                            | revenues                          | thousands, `$`    | 22                                     | 12                                     |
|                                             | cost of revenues                    |                            | cost_of_revenues                  | thousands, `$`    | 20                                     | 12                                     |
|                                             |                                     | marketing                  | marketing                         | thousands, `$`    | 14                                     | 12                                     |
|                                             |                                     | technology and development | technology_and_development        | thousands, `$`    | 14                                     | 12                                     |
|                                             |                                     | general and administrative | general_and_administrative        | thousands, `$`    | 14                                     | 12                                     |
| operating income                            |                                     |                            | operating_income                  | thousands, `$`    | 14                                     | 12                                     |
| other income (expense):                     |                                     |                            |                                   |                   |                                        |                                        |
|                                             | interest expense                    |                            | interest_expense                  | thousands, `$`    | 17                                     | 12                                     |
|                                             | interest and other income (expense) |                            | interest_and_other_income_expense | thousands, `$`    | 12                                     | 12                                     |
| income before income taxes                  |                                     |                            | income_before_income_taxes        | thousands, `$`    | 20                                     | 12                                     |
| provision for (benefit from) income taxes   |                                     |                            | -                                 | thousands, `$`    |                                        |                                        |
| net income                                  |                                     |                            | net_income                        | thousands, `$`    | 12                                     | 12                                     |
| earnings per share:                         |                                     |                            |                                   |                   |                                        |                                        |
|                                             | basic                               |                            | eps_basic                         | `$`               | 20                                     | 12                                     |
|                                             | diluted                             |                            | eps_diluted                       | `$`               | 12                                     | 12                                     |
| Weighted-average common shares outstanding: |                                     |                            |                                   |                   |                                        |                                        |
|                                             | basic                               |                            | wacso_basic                       |                   | 21                                     | 11                                     |
|                                             | diluted                             |                            | wacso_diluted                     |                   | 11                                     | 11                                     |
|                                             |                                     |                            |                                   |                   |                                        |                                        |


### Процесс создания датасета

1. Получить все ссылки на годовые финансовые отчеты на странице с отчетам (`BeautifulSoup`)
2. Скачать все отчеты (`selenium`)
3. Найти текст в таблицах `Consolidated statements of operations` и сохранить его в текстовые файлы (`pdfplumber`)
4. Преобразовать текст в таблицы
5. Переименовать стобцы в таблицах для последующего объединения
6. Объединить две таблицы и сохранить датасет

### Ограничения датасета
1. Рассматривались только таблицы `CONSOLIDATED STATEMENTS OF OPERATIONS`
2. Не полное объединение данных (использовались столбцы из таблицы за 2019 год)
