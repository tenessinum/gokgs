# Топ 100 игроков [gokgs]('https://www.gokgs.com/') и две их игры от команды черное&белое
Протестировать наше приложение можно [тут](http://89.208.199.114:5000/). 
Если адрес недоступен, напишите @KondakovaM в телеграм
## Описание структуры репозитория
Весь основной код находится в файле 
[`main.py`](https://github.com/Tennessium/gokgs/blob/main/main.py). 
Шаблоны находятся в папке [`templates`](https://github.com/Tennessium/gokgs/tree/main/templates)
, `*.css` в папке [`static/css`](https://github.com/Tennessium/gokgs/tree/main/static/css), 
файлы для библиотеки WGo.js в [`static/wgo`](https://github.com/Tennessium/gokgs/tree/main/static/wgo)
## Описание методологии взаимодействия API
 - Ники игроков для главной страницы получаем с [сайта](https://gokgs.com/top100.jsp) gokgs.
 - С помощью запроса JOIN_ARCHIVE_REQUEST узнаем информацию о двух последних играх, а также рейтинг и дополнительную информацию об игроке.
 - При переходе на страницу игры дополнительно запрашиваем ходы игры через
 ROOM_LOAD_GAME. Так как сервер предоставляет информацию в формате массива из SGF Events, немного парсим результат запроса и переводим в SGF строку, которую уже отображаем на странице
## Описание реализованной функциональности 
 Главная страница:

 ![Главная страница](https://github.com/Tennessium/gokgs/blob/main/docs/board.png "Главная")

 Описание есть в шапке страницы. Также напротив ника отображается информация, если игрок чаще играет с соперниками, которые сильнее его.
 
 Страница доски:

 ![Страница доски](https://github.com/Tennessium/gokgs/blob/main/docs/main.png "Доска")

 На странице отображается состояние доски в выбранный ход, оставшееся у игроков время, а также информация о пропуске хода.
## Видео демонстрация, подтверждающая работоспособность заявленного
[Сыллка на диск](https://drive.google.com/file/d/155RwzlIjuv-7Io004WSNI6dHCK32La1c/view?usp=sharing)
## Описание стека технологий и библиотек

Web приложение написано на [Flask](https://flask.palletsprojects.com/en/1.1.x/) с использованием библиотеки [WGo.js](https://github.com/waltheri/wgo.js/). 
Для некоторых элементов верстки использовался [Bootstrap](https://getbootstrap.com/). Запросы выполнялись с помощью python библиотеки [requests](https://docs.python-requests.org/en/master/). 
С парсингом главной страницы помог [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/). Для логирование используем [logging](https://docs.python.org/3/library/logging.html)
##  Схема архитектуры системы
Функции `login`, `logout`, `send` и вызов `requests.get` в функции `get_players `отвечают за работу с сетью. 

Класс game с функцией `load` получает полную информацию об игре и переводит её в формат для шаблона страницы доски.

`update_games` формирует данные для главной странички. `get_players` отвечает за парсинг странички gokgs.

`players_to_dict` отвечает за форматирование данных для главной странички. 

Также у приложения есть два обработчика пути и main с конфигурацией и стартом загрузки игр.