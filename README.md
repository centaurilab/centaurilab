
##Реализованные проекты автоматизации

###1. Система автоматического создания раскроя двери на основе заявки.

- Функции:

  - На основе данных из подтвержденной заявки от заказчика, используя БД предприятия
	программа выбирает необходимый шаблон подходящий для заявки (для разных типов дверей используются
	различные шаблоны), далее происходит ввод информации о изделии в шаблон(таких как - габаритные
	размеры, типы и количество замков, наличие и размеры оконных проемов,  вент.решеток, наличие и 
	количество анкерных и отверстий под противосъемы и тп.)
	
  - Выборка из заявки одинаковых изделий и объединение их в группу
  
  - На основе выборки создается каталог содержащий в своем имени номер наряд-заказа или диапазон наряд-заказов,
	тип изделия и его габаритные размеры. В который сохраняется созданный файл, с аналогичным названием,
	содержащий в себе развертки деталей, готовых для раскладке на листе. 
	
- Описание:

  - Данное программное обеспечение позволяет снизить нагрузку на технологов, исключить человеческий
	фактор при вводе информации из наряд-заказа в САПР, и существенно ускорить данный ввод,
	дает предупреждения если в заявке есть несоответствие или ошибка, пропущенная заказчиком 
	или менеджером обрабатывающим заявку. Работает путем считывания штрих-кода с наряд-заказа,
		в котором содержиться уникальный индетефикационный номер в БД, в которой содежится вся информация о заявке,
	далее создается файл с готовыми развертками деталей. Система позволила повысить
	производительность технологов с 20 просчетов в смену до 70, покрытие системы 87% заявок,
	что существенно снизило брак вызванный неправильной обработкой наряд-заказа.
        
        Реализация:
          - Python 3.8
          - API КОМПАС-3D v18.1
          - MySQL
          - PyQt 5

***

###2. Система резервирования порошковой краски.

- Описание:

  - После подтверждения заявки(счета), система на основе данных о площади всех изделий
    резервирует необходимое количество порошковой краски при этом учитываются
    условия использования только одного производителя для заявки, во избежание
    разницы цветов изделий; при наличии нескольких красок одного RAL, резервирование
    будет осуществлено для того производителя, краски которого, меньше всего на складе
    (выработка остатков). При прохождении изделия малярного цеха, происходит списание
    с резерва соответствующего количества порошка. Данные о наличии красок их количестве
    и резерве выводятся на web-страницу, в случае, когда происходит превышение резерва
    над фактическим количеством для лучешго восприятия информации, в таблице путем цветовой
    индикации сообщается о необходимости пополнить склад на этапе обработки заявки,
    это позволяет заблаговреммено составить заявку на краску заводу-производителю,
    тем самым снизить риск срыва сроков. Также позволяет отделу снабжения оперативно
    получать инормацию о текущем состоянии резервирования и наличия. 
    
        Реализация:
          - Python 3.10
          - Django framework
          - MySQL
          - PostgreSQL
***
			
		
###3. Система информирования.

- Описание:

  - Система разработана для получения оперативной информации о состоянии
        заявки, а так же о состоянии наряд-заказа. Система разработана в первую
    очередь для начальников смен и основана на Telegram боте - плюсы данного решения -
    доступность информации в любом месте и в любое время.
    Инормация о заявке содержит в себе распределение изделей по постам на текущий момент.
    
    Пример:

        Счет: №17
        Заказчик: ООО"Заказчик"
        1. Не запущены в работу - 16 шт.
        2. Лазеная резка - 5 шт.
        3. Гибочный станок - 7 шт.
        и тд.>

    Данное сообщение приходит ответом на запрос к телеграм-боту, альтернативой данному сообщению служит 
    выведение всего списка изделий в заявке и их состояний на рабочий принтер. В Отчете
    содержиться более детальная инфомация о состоянии счета.
    Информация о наряд-заказе содержит данные об исполнителях на каждом посту. Что позволяет
    при выявлении брака на конкретном изделии на месте определить всех исполнителей.
    Также это дает возможность в режиме реального времени видеть на каком этапе производства
    находиться изделие.
- Функции:
  - Отчеты 
    
    Вывод на рабочий принтер иформации о состоянии счета
  - Информация о конкретном наряд-заказе
  
    <img src="screen_unit.jpg" width="300">
  - Информация о счете
 
    <img src="screen_invoice_1.jpg" width="300">
    <img src="screen_invoice_2.jpg" width="300">
  - Прием смены
  - Состояние загрузки цеха
 
    <img src="screen_state.jpg" width="300"> 
  - Обновление используемой краски
  - Сообщение на панель сменного мастера
  - Выдача фурнитуры

        Реализация:
         - Python 3.10
         - AIOgGram
         - MySQL
         - PostgreSQL
***
###4. Монитор начальника смены.


- Описание:

  - Простой веб-интерфейс в котором отображена таблица, содержащая в себе информацию
    о запущенных в работу счетах. Таблица содержит такие поля как номер счета, заказчик,
    приоритетность, количество изделий в счете, и суммарный процент готовности всех изделий внутри счета.
    Данный интерфейс интегрирован с Системой Информирования - позволяет начальнику производства
        в режиме реального времени задавать приоритеты для определенных счетов.
   
    <img src="screen_masterdesk.jpg">
    
        Реализация:
         - Python 3.10
         - Django framework
         - MySQL
         - PostgreSQL
		
***
###5. Система складского управления.
- Описание:

  - Простой веб-интерфейс в котором отображена таблица, содержащая в себе информацию
    о запущенных в работу счетах. Таблица содержит такие поля как номер счета, заказчик,
    приоритетность, количество изделий в счете, и суммарный процент готовности всех изделий внутри счета.
    Данный интерфейс интегрирован с Системой Информирования - позволяет начальнику производства
        в режиме реального времени задавать приоритеты для определенных счетов.


	    
