Phalcon и Zephir
================

### Фото

http://cs417629.vk.me/v417629163/dfb2/zlCdi34xpg0.jpg

### Ссылки

https://github.com/ovr
http://dmtry.me/
https://twitter.com/ovrweb

### 3.

После более чем четырёх лет программирования в сфере веб-технологий окунулся в разработку OpenSource-приложений. Больше года принимаю активное участие в разработке Phalcon Framework и языка Zephir. Люблю есть зефир ;)

### 4.

Сладкое будущее: Phalcon и Zephir

### 5

C момента появления первых расширений к PHP в виде Си-фреймворков они успели наделать немало шума. 
Поговорим о фреймворке, лидирующем в данном направлении - Phalcon. Затронем его прошлое, настоящее и будущее; плавно перейдем к обсуждению языка программирования Zephir. Затронeм как синтаксис языка, так и его "внутренности": способы работы, алгоритмы анализа кода и методы, применяемые при оптимизациях. Проведем анализ данного решения: рассмотрим как производительность, так и другие важные качества, подведем итоги. Ну а завершим все это рассмотрением планов на будущее.

### 6

- Phalcon 1/2
- Производительность
- Zephir/ Зачем? Как устроен?
- Что скрывается внтури Zend Engine
- Zephir Kernel?
- Zephir Runtime?
- Phalcon/Zephir планы на будущее
   
### 7

Программисты PHP. От среднего и выше

###

Лесоруб

###

ООО "Лес"


## Набросок спитча (с ошибками, не правил)

Хей. Всем привет меня зовут Пацура Дмитрий
Я активный разработчик из сообщества Zephir и Phalcon.
Собственно в реальной жизни Работаю фулл стек веб разработчиком на аутсорсе но преиумществено в занимаюсь написании/оптмизированием бекенд систем (в частности REST API).
Но сегодня речь пойдет не обо мне.

Мой рассказ будет посвещен замечательно фрейморвку Phalcon (фалкон) и языку программирования Zephir.


> В ближайшие 30 минут

Но перед тем как начать мы посмотрим на план доклада и узнаем что предстоит нам послушать сегодня

В ближайшие 30 минут

Я расскажу вратце О Мире Cи фреймворков для PHP
Затрону Phalcon 1 версии (узнаем плюсы и минусы. посмотрим анализ производительности. заглнем внутрь.)
Плавно перейдем к Zephir (поговорим о назначении языка. о его возможностях особенностях. познокомимся с методами оптимизации производительности.)
Затем вернемся к Phalcon но уже 2 версии
И в конце нас ожидают подвидение итогов и рассказ планов на будущее данных технологий.

Итак начнем.

> Начнем с краткой вставки

Фреймворки на си для PHP это своеобразный сложийвский тренд рожденный фреймворком yaf (yet another framework)(соовсем другой фреймворк)
Это иикрофреймворк от PHP core team разработчка с никнеймом @лауренс, по этому я упомину его сдесь для того что бы люди знали первопроходца в данном направлении

На времена PHP 5.2 уже можно было достичь 16k RPM yaf-ом, где symfony 2.0 набирал около 3-4k RPM
разница в 4 раза. в 4 больших раза.
фреймворк был практически клоном Zend первой версии. начиная от структуры заканчиваю полным переписывание честей.

но так сложилось что в связись с малой заинтеревоностью автора и нежеланием активно заниматься разработкой
мы получили другого лидера в данном направлении, а именно Phalcon

> Сообствено Phalcon - это веб-фреймворк с высокой производительностью и низким потреблением ресурсов, собранный в виде Си-расширения для PHP.

> Плюсы

Конечно же из описания становиться ясным что благодаря более низкой реализации деталей на другом уровне байткода
Мы получаем хорошую производительность и при выносе алгоритом более низкое потребление памяти что может не радовать.
Простоста использования (это наверное очень хороший плюс позволяющий уже начинающему PHP программисту писать на нем)
Наличие готовых решение (да сообщества предлагает множество решение начиная от скелетон заканчивая готовыми сборками под вагрант для скорейщего и удобно старта с Phalcon)
Больщая универсальность (можешь делать рест апиай сервис можешь full mvc. как простой через 1 неймспейс так и через мультумодульную архитектуру)

о плюсах повогорили тепер переходим к минусам.

> Минусы

Наверное сейчас когда я начинаю озвучить минусы такие как

Сложность Разработки\Исправление\Отладка становиться ясным

что это те самые минусы которые присущи проектам на языке программирования Си

> Производительность

Ну а теперь для более наглядности я сделал график
Тестирование производилось PHP 5.6 в режиме fpm SAPI и включеным опкешом в ядре.
В первом графики я сравниваю фулл фреймворки. мультумодульные приложения.
На втором уже в micro приложениях.

> Что внутри?

- Конечно же смотря на код написанный на языке программирования Си, это вселяет некий ужас но это еще не так страшно как работа с внутриностями PHP

Каждый раз когда как я озвучиваю словосочитание внтуриности PHP я подсознантельно произношу Zend Engine.
Это сообствено и есть ядро PHP (виртульная машина). Для си разработчиков можно упоминуть что библиотека представляет API в виде набор функций обвернутые в макросы для сохранения совместимости в коде.
Сейчас это 2ая версия на момент 5 версии PHP.
И конечно же уже есть 3 версия разрабатывая в рамках PHP 7 или как ее называют phpng (php new generation)

Стоит оговориться что за парсинг анотаций и PQL (phalcon query language) у нас отвечают отдельно написанные парсеры
на flex и lemon.

Окей, что то я разговорился не буду многословным давайте же взгленем на код внутри

> Смотрим код

@поясняю

> Си для PHP разработчика это сложно

Ну сообствено наверное уже ясно
Си как язык программирования сложен, а для PHP разработчика это может показаться некрасивым и слишком низкоуровневым.
Не часто встретишь PHP разработчика имеющего опыт в написание не элементарных вещей на Cи но более
того задача разработки рассширений осложнена тем что в их написании стоит учитывать

"Понимания кухни PHP изнутри"

но даже не это главное как имение практического опыта.

в "Работе c Zend Engine"

=======


Ну а все таки. Проблему стоит пробывать решать, а именно дать PHP разработчику возможность писать на близком ему языке
А решение этой задачи становиться DSl

> Это DSL

Для более ярких примеров я выбрал 2 языка - Java и Javascript и их DSL

Для Java это ***
Для JavaScript это **


Для многих языков DSL трансляторы существует

> Ну а что же для Zend Engine?


> Zephir

Слово Zephir - это можно сказать склеиная абревиатура от слов Ze(nd Engine) Ph(p) I(nt)r(mediate)

Ну и сообствено

Zephir — это высокоуровневый язык программирования с открытым исходным кодом для быстрого и простого создания PHP расширений.
Сообствено это транслятор.

> Теперь перейдем как же он устроен из нутри?

Само ядро написанно конечно же на PHP, но для парсинга мы используем отдельно написанный парсер на Си.
Кому интерестно для разбития на токены мы используем flex, а для синтаксического анализа Lemon.
Это небольшая концепция парсера от создателей sqlite. После всего процесса парсинга мы получаем дерево в формате json.

> Самые видимые различия

Перед тем как начить говорить об особенностях языка, следует поговорить об отличиях
Конечно же начну с самых ярких в сравнении с PHP

> 1 пункт

Не нужно писать шорт теги. Для открытия и закрытия файла.

> 2 пункт

Прощай $ я конечно же имею об назойливом символе а не деньгая разработчика :)

> Переменная должна быть обьявлена перед использованием

Не обезательно делить это на 2 строки
обьявляться а только уже в следущей строке писать значение по умолчанию


Окей видимые различия с PHP мы знаем теперь переходим к особеностям

> Особенности

#### Статически/Динамическое программирования.
Динамический тип переменной мы обьвяляем с ключевого слово var. А для статического четко указываем тип.
int char float bool. Стоит обговорить то что мы работает с ядром Zend Engine и в случаии чего транслятор может безприпятсвенно конвертировать
наш статический ти уже в Zval.

#### Безопасная работа с памятью

Как многим наверное известно в си у нас есть различные структуры для передования значений. Это указатели, ссылки.
А так же в си и с++ мы должны сами выделять память для наших значений на которые указывает указатель.

Так зефир избавляет нас от необходимости выделения и освобождения памяти. Мы просто пишим код не думает об этом.
А сам транслятор делает это за нас.

Это сделано благодаря подходу "Кадровой памяти" - так называемых Memory frame.

При страте выполнения метода\функции у нас создается фрейм. описываем указатели. выделяется память под переменные. устанавливаем значения.
а уже в конце метода происходит закрытие фрейма с возможность вытеснения сразу или уже после выполнения скрипта.

#### Aheod of time

Сообствено во время компиляции мы оптимизируем и реарганизуем код для большей эфективности.


Ну сообствено после рассказа об особеностях языка. я считаю долгом рассказать об оптимизациях.

>

Наверное для большей наглядности я приведу достаточно широкоизвестный математичиский ряд и функцию для нахождения его
а именно

> Числа Фибоначчи

Как известно для нахождения этого ряда используют рекурсивный подход

## Особености

## Возможности

Ну а теперь на десерт, мы поговорим о сладком будущем Zephir и Phalcon но начнем с Zephir

> Будущее Zephir

### Больше оптимизаций

Мы будем проводить как оптимизацию выходного транслируемого кода так же и оптимизацию самого транслятора и увелечение кодовой базы.
По мимо этого у нас есть своя библиотека называемая Zephir Kernel которая позволяет
упростить разработку рассширения но так же и увеличить скорость работы используя оптимизации на уровни си кода не вызвая функцию и стандартного
рассширения PHP.

### Переработка архитектуры на раздельные компоненты

За время разработки у нас накопился список из мест на которые стоит обратить внимания.

Но из глобального Мы хотим разбить и доработать а местами переработать текущию архитектуры что бы она представляла из себя
слабосвязанные взаимозаменяемые компаненты что бы в будущем получилось что то подобное

** Нужен слайд

Парсер Ядро Оптимизатор Кодогенарция

Где под кодогенерация я подрузумиваю бекенд а в нашем случаии какой то конкретный язык программирования
Сейчас для частного случая Zephir это си c Zend Engine и Zephir Kernel.

Исходя из этого планирует добавление

### PHP, Hack, PHP-CPP в роли бекенд серверов

что сообствено у меня на слайдет отмечано как ....

### Развития Zephir Runtime

Тут все просто доделать его до более менее рабочего состояния

### Возможно попробуем реализовать ZephirVM

Было бы интерестно в учебных целях сделать нечто подобное
Очень интерестно посмотреть на сколько можно и как сложно обогнать ядро PHP используя путь

Взять LLVM (Low level virtual machine) язык программирования C++ и реализовать базовые вещи.


Окей, настеч настоящего и ближайщего будущего Zephir мы разобрались. Давайте вернемся к Phalcon но уже 2 версии
Сообствено очевидно что Phalcon 2 версии написан на Zephir

> Какая разница между 2 и 1 версией

Вообще для программиста внтури приложения они на 99.999% совместимы за исключением пару мест. где добавились интерфейсы ну и декларация типов улучшена.
Улучшена кодовая база. Раньши при написании кода на си в некоторых местах было странное впечатление что код писали настощие роботы
причем понять что где когда было тяжело. сейчас все наглядно и понятно.
Конечно же улучшли тесты: дополняя их и исправляя.

>



> Производительность Phalcon 2

Уже для тестов я взял настоящее приложение. Где есть нормальные модели. работа с бд. работа с memcache.
Тестирование производилось для 1 ноды с PHP версии 5.6.6 вкл опкешом.

Для чистой работы Phalcon2  у меня вышло около NNN rps но так как я не считаю работу с ней достаточно удобной то я перешел со времени на стек
фалкон 2 и doctrine 2 в качестве ORM = результат уже NNN что существено ниже но быстрее и удобнее в разработке.
Конечно же у меня оставался еще 1 хороший вариант это диманизировать приложение
Для этих целей я написал свой process manager на пхп.
Для работы я выбрал стратегию форка процессов (создание воркеров) а внтури воркера я использовал евент луп система благодаря библиотеке
reactphp. Результат уже NNN rps.

РРР RPS это ННН k рпм

Конечно заверщая свой спитч хочеться сказать что большая часть производительности приложения закладывается и 
зависит от его грамотно построенной архитектуры и вовремя продуманой архитектуры.
Но и архитектура состоит из различных инструментов: фреймворках серверах баз данных серварах поиска индексирования колейкций веб прокси серверах.
И для роли фреймворка я думаю Phalcon 2 является достаточно хорошим выбором сохраняя баланс между качеством кода и скорость вашего приложения

Ну а теперь вопросы...
