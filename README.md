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
В реальной жизни Работаю аутсорс разработчиком в разлиных компаниях преиумществено в написании оптмизировании бекенд рест систем.
Но сегодня речь пойдет не обо мне.

Мой рассказ будет посвещен фрейморвку Phalcon (фалкон) и языку программирования Zephir.


> В ближайшие 30 минут

Но перед тем как начать мы посмотрим на план спитча и узнаем что предстоит послушать

В ближайшие 30 минут

Я расскажу О Мире Cи фреймворков для PHP 
Затрону Phalcon 1 версии
Плавно перейдем к Zephir но затем вернемся к Phalcon но уже 2 версии
И в конце нас ожидают подвидению подвидение итогов

Итак начнем.

> Начнем с краткой вставки

Фреймворки на си для PHP это своеобразный сложийвский тренд рожденный фреймворком yaf (yet another framework)
Микрофреймворк от PHP core team разработчка лауренс, по этому я упомину его сдесь для того что бы люди знали первопроходца в данном направлении

На времена PHP 5.2 уже можно было достичь 16k RPM где symfony 2.1 набирал около 3-4k RPM
разница в 4 раза. в 4 больших раза.

но в связись с малой заинтеревоностью автора и нежелание продолжать
мы получили другого лидера в данном направлении, а именно Phalcon

> Сообствено Phalcon - это веб-фреймворк с высокой производительностью и низким потреблением ресурсов, собранный в виде Си-расширения для PHP.

> Плюсы

Конечно же из описания становиться ясным что благодаря более низкой реализации вещей
Мы получаем хорошую производительность и при выносе алгоритом более низкое потребление памяти.

> Минусы

Наверное сейчас когда я начинаю озвучить минусы такие как

Сложность Разработки\Исправление\Отладка становиться ясным

что это те самые минусы которые присущи проектам на языке Си

> Что внутри?

- Конечно же код написанный на языке программирования Си, что вселяет некий ужас но это еще не так страшно как работа с внутриностями PHP

Каждый раз когда я озвучиваю словосочитание внтуриности PHP я подсознантельно произношу Zend Engine.
Это сообствено и есть ядро PHP. Для си разработчиков можно упоминуть что библиотека представляет набор функционал и набор макросов обворачивающий данных код
для сохранения совместимости.
Сейчас это 2ая версия на момент 5 версии PHP.
И конечно же уже есть 3 версия разрабатывая в рамках версии PHP 7 или как ее называют phpng (php new generation)

Окей, что то я разговорился не буду многословным давайте же взгленем

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


> Особенности

****

Поговорив об особеностях следует поговорить об отличиях
пожалуй об самых ярких

>

Прощай $ я конечно же имею об назойливом символе а не деньгая разработчика :)

> Переменная должна быть обьявлена перед использованием

Не обезательно делить это на 2 строки
обьявляться а только уже в следущей строке писать значение по умолчанию


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

> Производительность Phalcon 2


Конечно заверщая свой спитч хочеться сказать что большая часть производительности приложения закладывается и 
зависит от его грамотно построенной архитектуры и вовремя продуманой архитектуры.
Но и архитектура состоит из различных инструментов: фреймворках серверах баз данных серварах поиска индексирования колейкций веб прокси серверах.
И для роли фреймворка я думаю Phalcon 2 является достаточно хорошим выбором сохраняя баланс между качеством кода и скорость вашего приложения

Ну а теперь вопросы...
