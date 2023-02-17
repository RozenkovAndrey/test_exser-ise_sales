# Заказчик — компания по установке систем безопасности многоквартирных домов и умных домофонов. 

# Статус проекта: Завершен

# Описание проекта:

В проекте были определены и исправлены 3 вида отклонений, что помогло 245 пользователям не оплачивать услугу дважды и увеличить лояльность клиентов к компании.

# Использованные библиотеки
Python, Pandas, PostgreSQL(SQL), Seaborn

# Использованные данные:
Данные предоставлены заказчиком;

# Основные выводы:

По результату знакомства с таблицей ЛС и тарифами:

Типы данных по столбцам совпадают.

Явных дубликатов строк нет.

В столбце статус услуги 227 пропусков.

В столбце тарифы большинство пропусков связано с услугой по рассрочке за монтаж ВБ.

В столбце ИД Дома видно преобладание значений рядом с 5000, в столбце ставка тарифа преобладают значения от 5 до 6, в столбце Дата начала услуги со значением года от 2008 и ниже.

Более 75% тарифных планов ниже 5.4.

Большинство событий со статусами услуг произошло в 2006 и 2007 годах.

Как и ожидалось наиболее популярными оказались базовые услуги.

Большинство из представленных услуг активны.

Количество лицевых счетов (одинаковых или разных) в некоторых квартирах превышает 1. Это может быть связано со сменой тарифа и услуг пользователем, отключением/включением услуг.

Количество уникальных счетов и квартир совпадает, но как показала дальнейшая работа не обязательно что номер счёта совпадает с номером квартиры
Некоторые из базовых услуг повторяются по два раза для одного пользователя, что не должно быть по заданию. Это может быть связано с тем, что завершение услуги произошло давно и её забыли удалить. Также это может быть связано с дополнительными работами по технической части и устранением неполадок уже после первого технического отключения услуги.

Многие из повторяющихся базовых услуг со статусом завершена имеют разницу во времени год и более, некоторые достигают значения в 16 лет, а некоторые 4 дня назад. Так как - ТО домофонов и системы видео безопасности проводится раз в квартал, то старые значения, превышающие этот срок, можно удалить. Предыдущие значения, что не превышают срок 3 месяца, нужно тоже удалить, так как в дальнейшем они повлияют на расчёт стоимости услуг для клиентов и возникнет путаница какое значение из повторяющихся статусов верно.

Не известен дальнейший путь клиента после завершения услуги. После завершения услуги есть клиенты, которые перешли на другой тариф и услугу, есть - кто перестал пользоваться услугами вовсе, думаю есть и такие кто взял перерыв на какое - то время и потом опять возобновил пользование услугами. Например, при анализе данных посещения сайтом есть логи, в которых содержится информация о начале и конце сессии пользователя, должно быть зафиксировано и время завершения услуги по аналогии. Также думаю, что возникают сложности при учёте информации, вводимой в ручном режиме и меньше - там где происходит авто списание денежных средств.

Есть случаи, где услуга прекращена, но клиенты ещё платят, вероятно погашают долг или платят после прекращения услуги, в этом также стоит разобраться. Этот момент также невозможно отследить без даты прекращения услуги.

В таблице платежей пропуска только в столбце с комментариями, форматы данных в столбцах соответствуют
Два пользователя с отрицательной суммой платежа, хорошо бы сравнить с другими данными много это или мало для такой когорты.

Ввиду того, что не знаю дальнейший путь клиента после завершения услуги, удаляю всех пользователей со статусами отличными от активный и в дальнейшем пренебрегаю вычислениями, связанными с ними в ряде расчётов.

При соединении таблиц с ЛС и платежами есть аномалии, разность между датой выгрузки данных и датой начала услуги у некоторых пользователей отрицательная, почему такое могло произойти стоит разобраться, возможно при ручном вводе произошла ошибка или ошибка при выгрузке данных (таких пользователей было 245).

Судя по суммарной разнице между планируемой выручкой за период оплаты пользователями и суммарной оплатой пользователями за тот же период дебиторская задолженность организации перед пользователями составляет около -1.629.133,6 без учёта что со дня активации услуги она могла подорожать. Конечно, этот вопрос необходимо проработать более глубже, перепроверить расчёты с учётом специфики бизнеса и дополнительной информации. Из расчётов видно, что многие пользователи платят услуги наперёд.

Количество оплаченных тарифов за 2020 год для всех квартир 1, это может быть связано с тем, что один тариф может включать несколько услуг.

Платить постоянно небольшие суммы не удобно, большая часть клиентов оплачивает услуги 2 раза в год, возможно, если подобрать другой интервал и имеется возможность оплачивать услуги раз в год, то большая часть клиентов будет действовать именно так.

Платёжная дисциплину абонентов хорошо отражает метрика - средний чек по оплатам в месяц.

При визуализации метрики чётко прослеживается резкое увеличение среднего чека в месяцах декабрь и январь представленных годов, что показывает сезонность поступления прибыли. При добавлении автосписания пик в 2020 году увеличивается вверх по сравнению с 2020 годом без автосписания, что может возможно можно объяснить ковидными мерами и самоизоляцией в этом году и многие просто не выходили на улицу и оплачивали онлайн.

В другие годы скачка с автосписанием не наблюдается. Также пики подтверждают гипотезу, что большая часть пользователей оплачивает услуги раз в год.
