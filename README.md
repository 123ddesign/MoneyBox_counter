# Копилка со счётчиком монет
Электронный распознаватель монет (по размеру) для копилки со счётчиком суммы и статистикой по каждому типу монет.  
Функционал:
- Распознавание размера монет с высокой точностью и его привязка к стоимости каждой монеты
- Вычисление общей суммы монет в копилке
- Статистика по числу монет каждого типа
- Все настройки сохраняются в энергонезависимую память и не сбрасываются при питании
- Накопленная сумма тоже хранится в энергонезависимой памяти и не боится сбоев питания 
- Режим глубокого энергосбережения: в спящем режиме потребляется 0.07 мА, в схеме без преобразователя 0.02 мА
- Поддержка любого числа монет разного размера
- Автоматическая калибровка типов монет
- Сброс накопленного количества  
- Подробности в видео: https://youtu.be/lH4qfGlK2Qk

# Table of Contents
  * [Chapter 1](#chapter-1)
  * [Chapter 2](#chapter-2)
  * [Chapter 3](#chapter-3)

## Папки
- **Библиотеки** - библиотеки для дисплея и прочего, скопировать в  
`C:\Program Files (x86)\Arduino\libraries\` (Windows x64)  
`C:\Program Files\Arduino\libraries\` (Windows x86)
- **money_box_counter** - прошивка для Arduino, файл в папке открыть в Arduino IDE (читай FAQ)

## Схема питания от USB
![СХЕМА](https://github.com/AlexGyver/MoneyBox_counter/blob/master/scheme1.jpg)

## Схема питания от аккумулятора через мосфет
![СХЕМА](https://github.com/AlexGyver/MoneyBox_counter/blob/master/scheme2.jpg)

##  Материалы и компоненты
Если товар закончился, то почти всё указанное ниже можно найти здесь http://alexgyver.ru/arduino_shop/ или здесь http://alexgyver.ru/electronics/

* Arduino NANO http://ali.pub/1qqtjx
* Дисплей http://ali.pub/oitu5
* Датчик http://ali.pub/1kamf3
* Повышайка http://ali.pub/1ingxt
* Кнопки и прочее http://alexgyver.ru/electronics/
* Мосфеты (список подходящих: IRF3704ZPBF, IRF3205PBF, IRLB8743PBF, IRL2203NPBF, IRLB8748PBF, IRF3704PBF, IRL8113PBF, IRL3803PBF, IRLB3813PBF, IRL3502PBF, IRL2505PBF, IRF3711PBF, IRL3713PBF, IRF3709ZPBF, AUIRL3705N, IRLB3034PBF, IRF3711ZPBF)
* Фототранзисторы отдельные: L-7113P3C, L-53P3C
* Светодиоды отдельные: L-7113F3C, L-53F3C

## Вам скорее всего пригодится
* Всё для пайки (паяльники и примочки) http://alexgyver.ru/all-for-soldering/
* Недорогие инструменты http://alexgyver.ru/my_instruments/
* Все существующие модули и сенсоры Arduino http://alexgyver.ru/arduino_shop/
* Электронные компоненты http://alexgyver.ru/electronics/
* Аккумуляторы и зарядные модули http://alexgyver.ru/18650/

## Как запустить и настроить
* Загрузка прошивки http://alexgyver.ru/arduino-first/
* Нажать и удерживать кнопку калибровки, затем подать питание/перезагрузить Arduino
* Если отпустить кнопку калибровки, система перейдёт в режим калибровки
* Если удерживать ещё 3 секунды - режим очистки памяти (сброс числа монет)
* После окончания калибровки система сама перейдёт в обычный режим работы

## Настройки в коде
    #define coin_amount 5    // число монет, которые нужно распознать
    float coin_value[coin_amount] = {0.5, 1.0, 2.0, 5.0, 10.0};  // стоимость монет
    String currency = "RUB"; // валюта (английские буквы!!!)
    int stb_time = 10000;    // время бездействия, через которое система уйдёт в сон (миллисекунды)

##  FAQ
### Основные вопросы
В: Как скачать с этого грёбаного сайта?  
О: На главной странице проекта (где ты читаешь этот текст) вверху справа зелёная кнопка **Clone or download**, вот её жми, там будет **Download ZIP**

В: Скачался какой то файл .zip, куда его теперь?  
О: Это архив. Можно открыть стандартными средствами Windows, но думаю у всех на компьютере установлен WinRAR, архив нужно правой кнопкой и извлечь.

В: Я совсем новичок! Что мне делать с Ардуиной, где взять все программы?  
О: Читай и смотри видос http://alexgyver.ru/arduino-first/

В: Компьютер никак не реагирует на подключение Ардуины!  
О: Возможно у тебя зарядный USB кабель, а нужен именно data-кабель, по которому можно данные передавать

В: Ошибка! Скетч не компилируется!  
О: Путь к скетчу не должен содержать кириллицу. Положи его в корень диска.

В: Сколько стоит?  
О: Ничего не продаю.

### Вопросы по этому проекту
В: На дисплее ничего не отображается!  
О: Покрути регулировку контраста сзади платы дисплея
  
В: На дисплее вместо текста отображаются белые прямоугольники!  
О: У твоего дисплея другой адрес, вот тут `LCD_1602_RUS lcd(0x27, 20, 4);`  
замени 0x27 на 0x3f ( *подсказка: `LCD_1602_RUS lcd(0x3f, 20, 4);`* )
  
В: А где ссылка на маленький дисплей?  
О: http://alexgyver.ru/arduino_shop/  дисплей OLED
  
В: При отключении акб или его полном разряде ведь счетчик монет сбросится?  
О: Нет, ты видео чем слушал?
  
В: Почему может не калиброваться? все перепробывал. Не распознает монеты?  
О: Возможно криво стоит датчик. В скетче есть режим отладки, раскомментируй его
  
В: Можно ли замутить ввод суммы кнопками?  
О: Можно, замути, мне некогда
  
В: Можно ли использовать фоторезистор?  
О: Инфракрасный? Если найдёшь - можно



## Chapter 1 <a id="chapter-1"></a>
Content for chapter one.

## Chapter 2 <a id="chapter-2"></a>
Content for chapter one.

## Chapter 3 <a id="chapter-3"></a>
Content for chapter one.