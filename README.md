![PROJECT_PHOTO](https://github.com/vvip-68/GyverPanelWiFi/blob/master/proj_img.jpg)
# Крутая WiFi панель на esp8266 своими руками
* [Описание проекта](#chapter-0)
* [Папки проекта](#chapter-1)
* [Схемы подключения](#chapter-2)
* [Материалы и компоненты](#chapter-3)
* [Как скачать и прошить](#chapter-4)
* [FAQ](#chapter-5)
* [Полезная информация](#chapter-6)

<a id="chapter-0"></a>
## Описание проекта
  
Этот проект основан на проекте ["Крутая WiFi лампа на esp8266 своими руками"](https://github.com/vvip-68/GyverLampWiFi)
с расширением возможностей работы на неквадратных широких матрицах с размерами более 26x12.  
Основное назначение проекта - настенные экраны больших размеров или гирлянды на широкие балконы.  
Также пожходит с некоторыми ограничениями для матриц с размерами 16x16.
Ограничение связаны с невозможностью отображения часов крупным шрифтом 5x7 для которого требуется матрица не менее 26 пикселей по ширине.
Для матриц менее 26 колонок шириной в часах может использоваться только шрифт 3x5 для которого достаточно 15 колонок.

### Железо
- Проект собран на базе микроконтроллера ESP8266 в лице платы NodeMCU или Wemos D1 mini (неважно, какую из этих плат использовать!)
- Реализована поддержка микроконтроллера ESP32, имеющего больший размер оперативной памяти и быстродействие, что позволяет управлять матрицами с большим количеством светодиодов
- Матрица может быть реализована на адресной ленте или отдельных светодиодах WS8212b, спаянных в нити гирлянды проводами
- Также для компактных панелей может использоваться соединение нескольких гибких адресных матриц 16×16, состоящих из 256 диодов с плотностью 100 штук на метр, что позволяет 
  легко получить матрицы размерами 32х16, 48x16, 64x16 и так далее
- Система управляется со смартфона по Wi-Fi, а также “оффлайн” с кнопки на корпусе (сенсорная кнопка на TTP223 или любая физическая кнопка с нормально разомкнутыми контактами)
- В случае реализации проекта в виде большой настенной матрицы поддерживается функционал будильника-рассвет и индикация текущего времени на индикаторе TM1637, 
  что позволяет в ночное время полностью выключать саму матрицу, оставляя возможность отображения текущего времени на этом индикаторе
- Поддерживается загрузка файлов анимации формата \*.out программы Glediator с SD-карты.

### Фишки
 - Более 40 крутых эффектов с поддержкой отображения часов или текста бегущей строки поверх эффектов
 - Регулировка яркости эффектов относительно яркости часов или текста бегущей строки, отображаемых поверх эффектов
 - Возможность задание до 36 разных текстовых строк, задание порядка их "воспроизведения" a также параметров отображения.  
   Тексты задаются из программы на смартфоне без необходимости перепрошивки контроллера.
 - Поддержка текста бегущей строки с отображением оставшегося до события времени, например: "До Нового года осталось 5 дней 12 часов"
   и после наступления события - вывод специального текста, например: "С Новым 2020 годом!!!"
 - Текст бегущей строки может отображаться различными цветами внутри одной строки.
 - Настройка скорости и вариаций отображения для каждого эффекта со смартфона
 - Поддержка эффектов анимации, подготовленных в программе “Jinx!”, сохраненных на SD карту
 - Работа системы как в локальной сети, так и в режиме “точки доступа”
 - Система получает точное время из Интернета
 - Управление кнопкой: смена режима, настройка яркости, вкл/выкл, отображение текущего IP адреса устройства
 - Режим будильник-рассвет: менеджер будильников на неделю в приложении
 - Отображение текущего времени на индикаторе TM1637
 - Отображение текущего времени на матрице поверх эффектов
 - Отображение текстовых сообщений на матрице поверх эффектов
 - Настройка сервера синхронизации времени из программы на смартфоне 
 - Установка текущего времени со смартфона вручную, если не удалось подключиться к серверу времени NTP
 - Два режима работы индикатора времени TM1637 - светится постоянно или выключается вместе с панелью
 - Пока время не получено с сервера NTP - на индикаторе TM1637 отображается --:-- вне зависимости от настройки
   "Выключать индикатор при выключении панели"
 - Поддержка звука будильника / звука рассвета звуковой платой MP3 DFPlayer
 - Настройки сетевого подключения (SSID и пароль, статический IP) задаются в программе и сохраняются в EEPROM
 - Если не удается подключиться к сети (неверный пароль или имя сети) - автоматически создается точка подключения
   с именем PanelAP, пароль 12341234, IP 192.168.4.1. Подключившись к точке доступа из приложения
   можно настроить параметры сети. Если после задания параметиров сети WiFi соединение установлено - 
   в приложении на смартфоне виден IP адрес подключения к сети WiFi.
 - Отображение текущего IP адреса устройства на индикаторе TM1637 или на матрице в режиме бегущей строки
 - Быстрое включение популярных режимов из приложения
 - Четыре программируемых по времени режима, позволяющие, например, настроить автоматическое выключение панели в ночное время
   и автоматическое включение панели вечером в назначенное время
 - Получение текущей температуры воздуха и погоды с сервера Yandex.Погода; Полученные данные могут отображаться в бегущей строке  
   Код региона (города) - из таблицы Яндекс.Погода - https://tech.yandex.ru/xml/doc/dg/reference/regions-docpage/

#### Эффекты:
 - Заливка панели белым или другим выбранным цветом
 - Снегопад
 - Блуждающий кубик
 - Пейнтбол
 - Радуга (горизонтальная, вертикальная, диагональная, вращающаяся)
 - Огонь
 - The Matrix
 - Шарики
 - Конфетти
 - Звездопад
 - Шумовые эффекты с разными цветовыми палитрами
 - Плавная смена цвета заливки панели
 - Светлячки
 - Водоворот
 - Мерцание
 - Северное сияние
 - Циклон
 - Тени (меняющийся теневой рисунок на матрице)
 - Демо-версия игры Тетрис (автоигра без возможности управления)
 - Демо-версия игры Лабиринт (автоигра без возможности управления)
 - Демо-версия игры Змейка (автоигра без возможности управления)
 - Движущийся синус
 - Палитра (лоскутное одеяло) 
 - Имитация графического индикатора спектра, движущегося "в такт музыке". 
 - Вышиванка
 - Дождь
 - Камин
 - Водопад
 - Стрелки
 - Эволюция (симулятор жизни)
 - Погода (слайдшоу или отображение текущих погодных условия)
 - Отображение анимированых картинок
 - Фоновые узоры (нотки, сердечки, снежинки, зигзаги и т.п.
 - Анимация с SD карты

### Кнопка управления режимами, последовательность переключения:
#### Будильник сработал, идет рассвет или мелодия пробуждения
- Любое нажатие кнопки отключает будильник
#### Долгое удержание кнопки 
- При включенной панели - плавное изменение яркости
- При выключенной панели - включение яркой белой панели освещения
#### Однократное нажатие кнопки
- Включение / выключение панели. При включении возобновляется режим на котором панель была выключена.
#### Двухкратное нажатие кнопки
- Ручной переход к следующему режиму
#### Трехкратное нажатие кнопки
- Включение демо-режима с автоматической сменой режимов по циклу
#### Четырехкратное нажатие кнопки
- Включение яркой белой панели освещения из любого режима, даже если панель была "выключена" /для сборки типа "Лампа"/  
  Отображение IP адреса пенели на матрице и на индикаторе TM1637, если подключение к локальной WiFi сети установлено  /для сборки типа "Панель"/  
#### Пятикратное нажатие кнопки
- На индикаторе TM1637 и на м атрице отображается IP адрес панели, если подключение к локальной WiFi сети установлено /для сборки типа "Лампа"/


### Настройка бегущей строки:
#### Общие правила
- Поддерживается 36 строк, каждая строка имеет номер '0'..'9','A'..'Z'
- "Макрос" - последовательность управляющих конструкций, каждая из которых заключена в фигурные скобки, например '{Exx}'
- Если строка с индексом '0' начинается с '#' - строка содержит последовательностьстрок к отображению, например '#123ZYX'  
  Эта последовательность задает порядок отображения строк '1','2','3','Z','Y','X' и далее по циклу
- Если строка с индексом '0' начинается с '##' - строки отображаются в случайном порядке
- Если строка с индексом '0' НЕ начинается с '#' или '##' - это обычная строка для отображения
- Если строка пустая, начинается с '-' или содержит '{-}' - строка отключена и не отображается
- Суммарный размер всех заданных строк не должен превышать 1500 символов, в противном случае строки, выходящие за размер не сохранятся

#### Макросы 
- **{-}**   в любом месте строки означает, что строка временно отключена, аналогично '-' в начале строки
- **{#N}**  в любом месте строки означает, что после отображения этой строки будет немедленно отображена строка с номером N, где N - 1..35 или '1'..'9','A'..'Z'
- **{Exx}** строка отображается на фоне эффекта XX, где XX - номер эффекта. Эффект не меняется, пока строка не будет полностью отображена
- **{TS}**  отображать строку указанное количество секунд S
- **{NX}**  отображать строку указанное количество раз подряд N
- **{CC}**  отображать строку указанным цветом. С Цвет задается в web-формате #RRGGBB  
            Если в строке только один макрос цвета текста, расположенный **в спмом начале** или в **самом конце** строки - вся строка выводится указанным цветом  
            Если в строке содержится несколько макросов определения цвета или макрос задан посередине строки, строка выводится указанными цветами:  
  - от начала строки до первого макроса цвета - глобальным значением цвета, который задается в программе на телефоне в настройках бегущей строки
  - от позиции макроса цвета до следующего макроса цвета или до концв строки - цветом, определенным в макросе
            Специальные значения цветов:  
  -  #000001 - радужные буквы вдоль текста  
  -  #000002 - каждая буква отдельным цветом
- **{BC}**  отображать строку на однотонном фоне. Цвкт фона задается в формате #RRGGBB
- **{WS}**  вставить в строку текущее состояние погоды (ясно, пасмурно, дождь и т.п.)
- **{WT}**  вставить в строку текущую температуру
- **{D}**   отображать часы вида ЧЧ:MM на месте макроса
- **{D:F}** отображать часы в указанном формате F, гдее F может содержать в себе:  
  -    **d** или **D**       - день месяца в диапазоне от 1 до 31  
  -    **dd** или **DD**     - день месяца в диапазоне от 01 до 31  
  -    **ddd** или **DDD**   - сокращенное название дня недели (пон - вск)  
  -    **dddd** или **DDDD** - полное название дня недели (понедельник - воскресенье)  
  -    **М**                 - месяц от 1 до 12  
  -    **ММ**                - месяц от 01 до 12  
  -    **МММ**               - месяц прописью (янв - дек)  
  -    **MMMM**              - месяц прописью (января - декабря)  
  -    **y** или **Y**       - год от 0 до 99  
  -    **yy** или **YY**     - год от 00 до 99  
  -    **yyyy** или **YYYY** - год в виде четырехзначного числа  
  -    **h**                 - час в 12-часовом вормате от 1 до 12  
  -    **hh**                - час в 12-часовом вормате от 01 до 12  
  -    **H**                 - час в 24-часовом вормате от 0 до 23  
  -    **HH**                - час в 24-часовом вормате от 00 до 23  
  -    **m**                 - минуты от 0 до 59  
  -    **mm**                - минуты от 00 до 59  
  -    **s** или **S**       - секунды от 0 до 59  
  -    **ss** или **SS**     - секунды от 00 до 59  
  -    **t** или **T**       - первый символ указателя am/pm или AM/PM  
  -    **tt** или **TT**     - указатель am/pm или AM/PM  
- **{Rdate#N}** оставшееся до события время, где **date** - дата события в формате ДД.ММ.ГГГГ  
  Оставшееся время показывается в соответствии с правилами:  
  -   осталось более 7 дней - *'XX дней'*  
  -   осталось 7 дней и менее - *'XX дней XX часов'*  
  -   осталось менее 1 дня - *'XX часов XX минут'*  
  -   осталось менее 1 часа - *'XX минут'*  
  -   осталось менее 1 минуты - *'XX секунд'*  
  
  Если событие уже прошло, вместо строки, содержащей макрос показывается строка-заместитель с номером N, где N - индекс 1..35 или '1'..'9','A'..'Z'.  
  Для того, чтобы строка-заместитель не показывалась как обычная строка, не связанная с событием - она должна быть "отключена" - то есть - начинаться с '-' или иметь внутри макрос отключения '{-}'.  
  Если вы забудите откллючить строку-заместитель, она будет отключена автоматически при воспроизведении родительской строки-события.  
  Если строка-заместитель не указана - строка с наступившим событием не показывается.

### Номера эффектов для макроса {Exx}
- **1** - "Лампа"
- **2** - "Снегопад"
- **3** - "Кубик"
- **4** - "Радуга"
- **5** - "Пейнтбол"
- **6** - "Огонь"
- **7** - "The Matrix"
- **8** - "Шарики"
- **9** - "Звездопад"
- **10** - "Конфетти"
- **11** - "Цветной шум"
- **12** - "Облака"
- **13** - "Лава"
- **14** - "Плазма"
- **15** - "Радужные переливы"
- **16** - "Полосатые переливы"
- **17** - "Зебра"
- **18** - "Шумящий лес"
- **19** - "Морской прибой"
- **20** - "Смена цвета"
- **21** - "Светлячки"
- **22** - "Водоворот"
- **23** - "Циклон"
- **24** - "Мерцание"
- **25** - "Северное сияние"
- **26** - "Тени"
- **27** - "Лабиринт"
- **28** - "Змейка"
- **29** - "Тетрис"
- **30** - "Палитра"
- **31** - "Спектрум"
- **32** - "Синусы"
- **33** - "Вышиванка"
- **34** - "Дождь"
- **35** - "Камин"
- **36** - "Водопад"
- **37** - "Стрелки"
- **38** - "Анимация"
- **39** - "Погода"
- **40** - "Жизнь"
- **41** - "Рассвет"
- **42** - "Узоры"
- **43** - Эффекты с SD карты

<a id="chapter-1"></a>
## Папки
**ВНИМАНИЕ! Если это твой первый опыт работы с Arduino, читай [инструкцию](#chapter-4)**
- **libraries** - библиотеки проекта.
- **firmware** - прошивки
- **schemes** - схемы подключения компонентов
- **sounds** - звуковые файлы будильника для размещения на SD-карте
- **Android** - файлы с приложениями, примерами для Android и Thunkable

<a id="chapter-2"></a>
## Схема
### С сенсорной кнопкой
![SCHEME](https://github.com/vvip-68/GyverPanelWiFi/blob/master/schemes/scheme.jpg)
### С обычной кнопкой
![SCHEME](https://github.com/vvip-68/GyverPanelWiFi/blob/master/schemes/scheme_b.jpg)
### С SD картой
![SCHEME](https://github.com/vvip-68/GyverPanelWiFi/blob/master/schemes/scheme_c.jpg)

<a id="chapter-3"></a>
## Материалы и компоненты
### Ссылки оставлены на магазины
Полный список компонентов есть в статье https://alexgyver.ru/matrix_guide/
- NodeMCU http://ali.ski/RgD5P  http://ali.ski/_1FJZ
- Wemos D1 mini http://ali.ski/FuTgbO  http://ali.ski/Z9feWU
- Матрица 16x16 http://ali.ski/BCKQT  http://ali.ski/bRW14  http://ali.ski/X-tBrQ
- Адресная лента (для DIY матрицы) http://ali.ski/2dmOe_  http://ali.ski/rqgqdq  http://ali.ski/4Ma9iH
- Сенсорная кнопка http://ali.ski/aWQBAa  http://ali.ski/rsOrSB
- Резисторы http://ali.ski/UEez2
- БП 5V (брать 3A минимум) http://ali.ski/K-CThT  http://ali.ski/3UWXJ
- MP3 DFPlayer http://ali.onl/1gY1 http://ali.onl/1gY3
- Динамики http://ali.onl/1h3u http://ali.onl/1h3v
- Проводочки http://ali.ski/JQRler  http://ali.ski/_SuCF
- Плафон https://leroymerlin.ru/product/plafon-cilindr-18212968/

## Вам скорее всего пригодится
* [Всё для пайки (паяльники и примочки)](http://alexgyver.ru/all-for-soldering/)
* [Недорогие инструменты](http://alexgyver.ru/my_instruments/)
* [Все существующие модули и сенсоры Arduino](http://alexgyver.ru/arduino_shop/)
* [Электронные компоненты](http://alexgyver.ru/electronics/)
* [Аккумуляторы и зарядные модули](http://alexgyver.ru/18650/)

<a id="chapter-4"></a>
## Как скачать и прошить
* [Первые шаги с Arduino](http://alexgyver.ru/arduino-first/) - ультра подробная статья по началу работы с Ардуино, ознакомиться первым делом!
* Скачать архив с проектом
> На главной странице проекта (где ты читаешь этот текст) вверху справа зелёная кнопка **Clone or download**, вот её жми, там будет **Download ZIP**
* Установить библиотеки в  
`C:\Program Files (x86)\Arduino\libraries\` (Windows x64)  
`C:\Program Files\Arduino\libraries\` (Windows x86)
* **Подключить внешнее питание 5 Вольт**
* Подключить Ардуино к компьютеру
* Запустить файл прошивки (который имеет расширение .ino)
* Настроить IDE (COM порт, модель Arduino, как в статье выше)
* Настроить что нужно по проекту
* Нажать загрузить
* Скачать и установить на смартфон GyverPanelWiFi
* Пользоваться  

**Подробная инструкция [тут](https://github.com/vvip-68/GyverPanelWiFi/wiki/%D0%9F%D0%BE%D0%B4%D0%B3%D0%BE%D1%82%D0%BE%D0%B2%D0%BA%D0%B0-%D1%81%D1%80%D0%B5%D0%B4%D1%8B-%D0%B4%D0%BB%D1%8F-%D1%81%D0%B1%D0%BE%D1%80%D0%BA%D0%B8-%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%B0)**

## Важно
Если проект не собирается (ошибки компиляции) или собирается, но работает неправильно (например вся матрица светится белым и ничего не происходит) - проверьте версии библиотек. Данный проект рассчитан на работу с версииями библиотек поддержки плат ESP версии 2.5.2 и библиотеки FastLED версии 3.2.9 или более новую;

Если в качестве микроконтроллера вы используете Wemos D1 - в менеджере плат для компиляции все равно выбирайте **"NodeMCU v1.0 (ESP-12E)"**, в противном случае, если выберете плату Wemos D1 (xxxx), - будет работать нестабильно, настройки не будут сохраняться в EEPROM, параметры подключения к локальной сети будут сбрасываться каждый раз при перезагрузке, плата вместо подключения к локальной сети будет каждый раз создавать точку доступа.

<a id="chapter-5"></a>
## FAQ
### Основные вопросы
В: Как скачать с этого грёбаного сайта?  
О: На главной странице проекта (где ты читаешь этот текст) вверху справа зелёная кнопка **Clone or download**, вот её жми, там будет **Download ZIP**

В: Скачался какой то файл .zip, куда его теперь?  
О: Это архив. Можно открыть стандартными средствами Windows, но думаю у всех на компьютере установлен WinRAR, архив нужно правой кнопкой и извлечь.

В: Я совсем новичок! Что мне делать с Ардуиной, где взять все программы?  
О: Читай и смотри видос http://alexgyver.ru/arduino-first/

В: Вылетает ошибка загрузки / компиляции!  
О: Читай тут: https://alexgyver.ru/arduino-first/#step-5

### Вопросы по этому проекту

В: Эй чувак! У тебя проект не компилится. Ты файл FastLed.h в проект забыл включить. Выложи!  
О: Это стандартная библиотека для FastLed для управления адресными светодиодами. Идите в менеджер библиотек и установите ее. Или скачайте с [сайта производителя](https://github.com/FastLED/FastLED)

В: Эй чувак! У тебя проект не компилится. Ты файл DFRobotDFPlayerMini.h в проект забыл включить. Выложи!  
О: Это стандартная библиотека для MP3 DFPlayer. Идите в менеджер библиотек и установите ее. Или скачайте с [сайта производителя](https://github.com/DFRobot/DFRobotDFPlayerMini)

В: Собрал, использую NodeMCU/Wemos. Ничего не работает! Мигает один или несколько светодиодов в начале матрицы. И всё.  
О: Производители разных плат (NodeMCU, Wemos) могут использовать различные схемы соединения контактов микроконтроллера ESP8266 к выводам макетной платы. Обычно используемый в проекте пин вывода на ленту приходится или на пин D2 или на пин D4. Для проверки не подключайте сигнальный провод матрицы к микроконтроллеру, вместо этого через резистор коснитесь вывода D2 или D4 пина микроконтроллера. Большая вероятность что матрица заработает с тем или иным вариантом подключения.

В: Собрал, использую NodeMCU. Эффекты работают, но нестабильно. Случайные вспышки на матрице. Буквы бегущей строки прыгают.  
О: NodeMCU v3 чрезвычайно требователен к источнику питания. Ему на вход VIN нужно подавать напряжение в диапазоне 4.7-5 вольт. И не более. Описанные эффекты возникают даже при питании в 5.25 (а тем более - 5.45) вольт. Для проверки - не подключайте +5 вольт от блока питания к NodeMCU совсем, питание подавайте на матрицу непосредственно. Землю NodeMCU и ленты соедините. Подключите сигнальный пин NodeMCU ко входу DIN ленты. Подключите NodeMCU к компьютеру через USB (питание будет поступать отсюда). Должно заработать. Далее регулируйте выходное напряжение своего блока питания.  
В особо тяжелых случаях, когда понижение напряжения питания системы не приводит к желаемым результатам и артефакты, вспышки, дрожание текста бегущей строки продолжается, можно использовать дополнительно схему преобразования уровня от 3.3 вольта с выхода NodeMCU к 5 вольтам входа адресной ленты:  
![SCHEME](https://github.com/vvip-68/GyverPanelWiFi/blob/master/schemes/convertor.png)

В: Не компилируется. Выбрана плата "голая ESP8266-12E". Сообщение об ошибке: "D4 was not declared in this scope."  
О: Очевидно производители библиотеки для "голой ESP8266-12E" не определили данную константу. Используйте вместо константы D4 числовое определение пина для вашей платы или выполните компиляцию проекта для плат NodeMCU или WeMos D1 mini.

В: Не компилируется. В сообщении об ошибке содержатся сведения о дублирующихся библиотеках.  
О: В вашей среде установлено две версии одной и той же библиотеки. Обычно это библиотека FastLED - одна версия находится в папке установки среды Ардуино (например в "C:\Program Files (x86)\Arduino\libraries\"), другая - в папке документов пользователя (например "C:\Users\vvip-68\Documents\Arduino\libraries\"). Удалите одну из версий библиотек и попробуйте скомпилировать снова.

В: Не компилируется. В сообщении об ошибке что-то про несоответствие типов.  
О: Обычно такая ситуация возникает в двух случаях:
- выбрана неверная плата. Используйте NodeMCU 1.0 (ESP-12E Module) или Wemos D1 mini. Под эти платы проект собирается, под другие, возможно, нужна модификация кода.
- установлена устаревшая версия библиотек поддержки плат - например для ESP8266 версия библиотеки 2.4.2. Данный проект использует библиотеки для плат ESP8266 версии 2.5. Обновите библиотеки поддержки плат.

В: Подскажите, что не так... C подключением через точку доступа всё исправно работает, а при попытке подключиться к локальной сети не могу законнектиться через приложение. В чем может быть проблема?  
О: Проблема может быть в неправильно указанном статическом адресе / параметрах сети в прошивке. В сектче по умолчанию используется адрес в сети 192.168.0.xxx. Ваш WiFi роутер в зависимости от настроек может создавать сеть в другом диапазоне. Чаще всего это 192.168.1.xxx или 192.168.100.xxx; Проверьте какую сеть создает ваш роутер и укажите в скетче и при подключении приложения к сети именно эту сеть.

В: Автор неверно указал IP адрес панели 192.168.4.1 в режиме точки доступа. На самом деле он 192.168.4.2 - указываю его, приложение на смартфоне подключается. Правда управлять устройством не получается все равно - она не реагирует на изменения.  
О: Нет, все правильно. IP панели - 192.168.4.1; Адрес 192.168.4.2 получает ваш смартфон при подключении к точке доступа. Когда в приложении для подключения вы указываете адрес 192.168.4.2 - вы подключаете ваш смартфон с самому себе, а не к устройству. Естественно никакое управление устройством работать не будет.   

В: Устройство создает точку доступа, телефон к ней подключается. В приложении ввожу IP адрес панели 192.168.4.1, но соединение не происходит. Что я делаю не так?  
О: Некоторые телефоны не могут передавать данные через точку доступа, пока в них активен мобильный интернет. Все передаваемые данные отправляются в интернет, вместо передачи их в точку доступа. В настройках телефона выключите мобильный интернет ("Мобильные данные"). После этого телефон из приложения должен подключиться к устройству.  

В: В скетче есть настройки который задают имя и пароль к локальной сети. Указываю, но к сети даже не пытается подключиться В чем дело?  
#define NETWORK_SSID ""                      // Имя WiFi сети - пропишите здесь или задайте из программы на смартфоне   
#define NETWORK_PASS ""                      // Пароль для подключения к WiFi сети - пропишите здесь или задайте из программы на смартфоне       
О: Эти настройки определяют параметры доступа к сети по умолчанию, которые используются при ПЕРВОЙ загрузке прошивки в устройство. В этот момент они сохраняются в EEPROM и при последующих запусках имя сети и пароль извлекаются из энергонезависимой памяти и используются уже извлеченные значения, а не те, что прописаны в #define. Если вы уже запускали устройство и ПОСЛЕ этого изменили в скетче имя и пароль сети, вам нужно также изменить значение флага, указывающее было ли уже сохранение параметров в EEPROM или еще нет. Этот флаг находится в файле a_def_soft.h в строке 9  
#define EEPROM_OK 0x5A                     // Флаг, показывающий, что EEPROM инициализирована корректными данными 
Измените его на любое другое значение, например 0xA5

В: Погода в Украине работать будет? Как узнать код региона для моего города?  
О: Зайдите на страничку yandex.ru  
В строке поиска наберите чего-нибудь, нажмите кнопку "Искать". Откроется страничка с результатами поиска.  
Смотрите что в адресной строке браузера. Там что-то типа https://yandex.ru/search/?lr=115326  
115326 - это код региона для которого яндекс отдает погоду. В Украине что-то возвращается?  
Далее этот код (в данном случае 115326) подставляется в этот запрос:  
https://yandex.ru/time/sync.json?geo=115326  
Если в ответ получено что-то вроде этого -  
{"time":1598783897149,"clocks":{"115326":{"id":115326,"name":"Фалькензе","offset":7200000,"offsetString":"UTC+2:00","showSunriseSunset":true,"sunrise":"06:15","sunset":"19:59","isNight":false,"skyColor":"#5ebdff","weather":{"temp":23,"icon":"bkn-d","link":"https://yandex.ru/pogoda/falkensee"},"parents":[{"id":103751,"name":"Бранденбург"},{"id":96,"name":"Германия"}]}}}  
погода работать будет. Если возвращается что-то другое - не будет.  


### Всё собрал строго по инструкции, ничего не работает.

1. Разбираем всё обратно.
2. Берем платку, смотрим чтобы к ней НИЧЕГО не было подключено.
3. Плату в таком состоянии подключаем кабелем USB к компьютеру.
4. Берем последнюю версию [прошивки](https://github.com/vvip-68/GyverPanelWiFi/) и загружаем ее в микроконтроллер.
5. Смотрим в сообщениях, что загрузка успешно выполнена и осуществлен перезапуск микроконтроллера, а в мониторе порта, что скетч стартовал, вывел версию прошивки, создал точку доступа PanelAP
6. Устанавливаем на смартфон приложение из этого проекта
7. Подключаемся телефоном к точке доступа, приложение подключаем к матрице, пробуем тыкать на кнопки.
8. Отключаем микроконтроллер от компьютера
9. Подключаем блок питания +5 вольт и минусовой провод к матрице. Минусовой провод подключаем также к пину GND микроконтроллера.
Контроллер подключаем USB кабелем к компьютеру, блок питания включаем в сеть.
10. Проверяем, что напряжение питания с блока не превышает +5.25 вольт. Если больше - регулируем его до уровня 4.8 вольта.
11. Сигнальным проводом с матрицы с подключенным резистором 200 Ом тыкаемся поочередно в пины D4 и D2 микроконтроллера. В каком-то из этих двух вариантов на иматрице должно сформироваться осмысленное отображение эффекта или бегущего текста. Что из этого конкретно должно в данный момент отображаться написано в мониторе порта. Запоминаем подключение к какому пину дало результат.
12. Отключаем микроконтроллер и блок питания. Провод +5V с блока питания подключаем к микроконтроллеру на пин его входного напряжения питания (у разных плат обозначен по разному - Vin, Vcc или +5). Сигнальный провод матрицы припаиваем к пину, который определили шагом выше. Очень желательно между пинами Vin и GND микроконтроллера припаять электролитический конденсатор номиналом 1000-4700 мкф, и параллельно ему керамический конденсатор на 33-100 нф.
13. Включаем блок питания в розетку. Панель должна заработать.
14. Собираем всю конструкцию в корпус. 

<a id="chapter-6"></a>
## Полезная информация
* [Cайт Alex Gyver](http://alexgyver.ru/)
* [Канал Alex Gyver на YouTube](https://www.youtube.com/channel/UCgtAOyEQdAyjvm9ATCi_Aig?sub_confirmation=1)
* [YouTube канал про Arduino](https://www.youtube.com/channel/UC4axiS76D784-ofoTdo5zOA?sub_confirmation=1)
* [Видеоуроки по пайке](https://www.youtube.com/playlist?list=PLOT_HeyBraBuMIwfSYu7kCKXxQGsUKcqR)
* [Видеоуроки по Arduino](http://alexgyver.ru/arduino_lessons/)
