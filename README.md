# Модуль планирования ресурсов учебного центра

**Ключевые задачи, решаемые модулем планирования:**
* распределение аудиторий учебного центра на основании годового плана-графика обучения
* распределение преподавателей учебного центра на основании плана-графика обучения
* определение доступного для продажи объема обучения в аудиториях учебного центра
* определение доступного для продажи объема выездного обучения

 **Функциональные блоки, которые должны быть реализованы:**
 * формирование справочников, необходимых для работы модуля:
     1. учебные программы,
     2. аудитории,
     3. преподаватели, их график сменности и график отпусков,
     4. учебная сетка (время начала и окончания пар).
  * управление расписанием занятий учебного центра (планирование и последующая корректировка с указанием причины внесения изменений) на основании годового плана-графика; определение доступных для продажи объемов услуг обучения,
  * интеграция с сервером Microsoft Exchange, позволяющая создавать события для каждого занятия, бронировать соответствующие помещения, приглашать преподавателей и отправлять приглашения преподавателям в корпоративную почту,
  * отметка факта проведения занятий,
  * WebAPI (программный интерфейс), предоставляющий данные в систему BI для дальнейшего построения отчетов. WebAPI должен поддерживать базовую авторизацию, формат передачи данных JSON. Состав передаваемых данных должен обеспечивать реализацию требований к отчетам в системе BI (см. пункт Требования к отчетам в системе BI по учебному процессу).
  * Требования к API (программному интерфейсу), который должен быть реализован в системе управления персоналом (HRM) для получения производственного календаря. В этом пункте необходимо сформировать только спецификацию: объектную модель API, перечень необходимых методов с описанием водных и выходных значений.
  
**Требования к отчетам в системе BI по учебному процессу**

Отчеты по учебному процессу должны предоставлять следующую информацию:
* процент занятий, проведенных в соответствии с первоначальным планом за выбранный период времени,
* общее количество групп, прошедших обучение за выбранный период времени,
* процент задействования аудиторий в занятиях за период времени,
* суммарное время проведенных преподавателями занятий за период времени,
* процент неиспользования аудиторий,
* процент неиспользованного рабочего времени преподавателей.

**Задачи, которые должен решать модуль планирования:**
* на основании годового план-графика (импортируется из Excel в модуль) расставить учебные группы по аудиториям на год, исходя из параметров аудиторий;
* на основании годового план-графика (импортируется из Excel в модуль) расставить преподавателей на каждый учебный день, исходя из параметров преподавателей;
* на основании данных по загрузке АУЦ на год прогнозировать возможные объемы продаж услуг (сколько слушателей можем подсадить в группы на базе АУЦ, сколько выездных групп можем организовать);
* создание отчетности в модуле (сколько групп проведено, процент загрузки аудиторий по месяцам, загрузка преподавателей в часах, процент неиспользованных ресурсов).

**Исходные данные:**
* производственный календарь (выходные и праздничные дни в году);
* годовой план-график обучения (Приложение №1);
* текущая программа управления расписанием (Архив «Расписание»);
* параметры аудиторий (Приложение №2);
* параметры преподавателей (Приложение№2);
* перечень учебных программ АУЦ (Приложение №2);
* учебно-тематические планы программ (Приложение №3);
* график сменности преподавателей (Приложение №4);
* график отпусков преподавателей (Приложение №5).
---
# Термины и сокращения
**Авиационный учебный центр (АУЦ)** — организация, осуществляющая обучение по программам, утвержденным Федеральным агентством воздушного транспорта (Росавиация), и программам, разработанным и утвержденным в соответствии с положениями Федерального Закона от 29 декабря 2012 г. № 273-ФЗ «Об образовании в Российской Федерации».

**Дополнительные профессиональные программы (ДПО)** — программы обучения, направленные на совершенствование и (или) получение новых знаний, умений и навыков, необходимых для профессиональной деятельности, и (или) повышения профессионального уровня в рамках имеющейся квалификации

**Дисциплина** – система знаний, умений, навыков, объединяющая несколько учебных программ одной тематики.

**Учебная программа** - созданный в рамках системы обучения документ, определяющий содержание и количество знаний, умений, навыков и уровня сформированности компетенций, предназначенных к обязательному усвоению по той или иной учебной дисциплине, распределение их по темам, разделам и периодам обучения, а также определяющий требования и критерии определения теоретических знаний и практических навыков Слушателей, необходимых для выполнения профессиональных обязанностей

**Вид занятий** – вид учебной деятельности (теоретические занятия, практические занятия в классе, практические занятия на производстве)

**Учебно-тематический план** – подробный план занятий с указанием разделов и тем в рамках каждой учебной программы

**Тема занятий** – единица измерения в рамках учебно-тематического плана программы, измеряется в академических часах

**Годовой план-график** – расписание учебных программ на год с распределением на группы по датам обучения, утвержденный руководством АУЦ

**Академический час (ак. час)** - отрезок времени продолжительностью 45 минут для занятий в учебных заведениях

**Учебная пара** – единица расписания занятий на день, составляет 1,5 часа

**Обязательное обучение у внешних лицензированных поставщиков** - обучение работников компании в других учебных заведениях на основании требований, предъявляемых отраслевыми нормативными документами, иными нормативными правовыми документами, по окончании которого выдается документ установленного образца, действующий определенный период времени

**СДО** - система дистанционного обучения 

**ВС** - воздушное судно

---

# Задача 1

### Составление годового план-графика обучения
Ежегодно в АУЦ составляется годовой план-график обучения в Excel с указанием точных дат обучения каждой группы по учебным программам. Необходимо предусмотреть инструмент интеграции файла Excel в Модуль. Более высокая сложность задания – разработать окно планирования годового план-графика прямо в системе с разделением года на недели (неделя 1,…неделя 52) и указанием выходных дней (суббота-воскресенье, праздничные дни). Разделение по неделям и выходные дни –динамическая информация, которая меняется ежегодно.

План-график так же меняется ежегодно. Даты обучения зависят от: 
* сезона обучения (осень, весна, лето, зима). В зависимости от сезона может быть снижена насыщенность расписания группами, так как летом все сотрудники заняты на производстве.
*	сроков окончания удостоверений работников. Каждое удостоверение по учебной программе имеет свой срок действия (от 2 до 5 лет), АУЦ обязан обучить работника не позднее даты окончания действия предыдущего удостоверения
*	объемов набора новых работников. Для новых работников обязательно прохождение учебных программ с пометкой «Базовый курс» в зависимости от должности

В ячейке каждой программы должна быть возможность отображения даты обучения (пример 03.04 - 07.04), а также аудитории. Информация должна отображаться по аналогии с визуализацией файла Excel, представленного в Приложении №1. 

### Автоматическое планирование ресурсов на обучение работников компании
На основании годового план-графика с датами обучения, Модуль автоматически распределяет учебные аудитории. Аудитории распределяются исходя из:
* необходимой для того или иного вида занятий конфигурации аудитории. Для теоретических занятий или практических занятий в аудитории- это аудитории с партами, для практических занятий – без парт;
* приоритетности аудитории для дисциплины. Существуют аудитории, которые закреплены за той или иной дисциплиной. Подробное описание представлено в Приложении № 2;
* свободных аудиторий на указанные даты;
* если совпадают темы занятий по разным учебным программам, то занятия проводятся в одной и той же аудитории;
* аудитория 422 должна быть задействована только в случае, если все остальные аудитории заняты.

На основании годового план-графика Модуль предварительно распределяет преподавателей на год на каждую учебную пару. Преподаватели распределяются исходя из:
* дисциплины, программы и тем занятий, по которым они могут проводить занятия;
* рабочего графика преподавателей;
* графика отпусков преподавателей;
* занятости преподавателей на других темах (в случае, если в один день совпадают темы занятий нескольких учебных программ – должен читать один преподаватель и должна быть задействована одна аудитория).

После предварительной расстановки преподавателей и аудиторий система отмечает красным цветом те учебные группы, на которые не хватает ресурсов (аудиторий и (или) преподавателей). Такие учебные программы пользователь Модуля распределяет вручную и переносит даты обучения/перераспределяет преподавателей.

---

# Задача 2

### Расчет пропускной способности АУЦ для обучения внешних заказчиков
После распределения ресурсов на обучение сотрудников Компании Модуль должен рассчитывать пропускную способность АУЦ по обучению внешних заказчиков. Внешние заказчики могут учиться тремя способами:
1. Добавлять своих работников в существующие группы для работников компании
2. Проводить выездные занятия на базе заказчика – в таком случае необходимое условие – это свободный преподаватель, готовый к командировкам.
3. Добавлена новая учебная группа на базе АУЦ при наличии свободных аудиторий и преподавателей. Данный способ используется только в случае, если пункты 1 и 2 невозможны.

Экономически наиболее выгоден вариант номер 2, когда проводится выездное обучение для группы, далее следует вариант номер 1. 

Пропускная способность для обучения внешних заказчиков рассчитывается исходя из:
* наличия свободных мест в группах, исходя из максимальной вместимости аудитории;
* наличия свободных аудиторий;
* наличия свободных преподавателей, готовых к командировкам.

По результатам расчета Модуль формирует второй план-график в отдельном окне с прогнозом по обучению внешних заказчиков. В план-графике создать цветовую индикацию, которая позволит отличить способ обучения (работники добавлены в существующие группы, добавлена новая учебная группа в АУЦ, выездная группа). Необходимо предусмотреть возможность просмотра данных в нескольких разрезах по каждой учебной программе отдельно: количество работников, которых мы можем добавить в существующие группы; количество выездных групп, которые можем провести.

--- 

# Навигация
По репозиторию:
* [Папка с данными](https://github.com/practicingfutures/Pulkovo.Hack_task/tree/master/data)
* [Полное описание модуля планирования учебного центра](https://github.com/practicingfutures/Pulkovo.Hack_task/blob/master/%D0%A3%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5%20%D1%80%D0%B5%D1%81%D1%83%D1%80%D1%81%D0%B0%D0%BC%D0%B8%20%D0%90%D0%A3%D0%A6_%D0%A2%D0%97.DOCX)

По хакатону:
* [Чат хакатона](https://t.me/joinchat/Sf_6iVTVeEKLqo_u74DVeg)
* [Канал хакатона](https://t.me/pulkovohack_info)
