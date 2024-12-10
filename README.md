## HELLO_API_TMDB

#### Служит для выявления проблем с доступностью сайта и корректностью API-ключа

Для запуска достаточно команды 

`python3 hello_api_TMDB.py`

При запуске скрипт запрашивает у пользователя ключ API, делает запрос к [сайту](https://www.themoviedb.org/) про фильм с номером 215, и выводит в терминал его бюджет. В случае, если API-ключ не был введён, пользователь увидит сообщение `Invalid api key`, и скрипт прекратит работу.

Для запуска необходим ключ API, для его получения необходимо зарегистрироваться на [сайте](https://www.themoviedb.org/) и пройти по [ссылке](https://www.themoviedb.org/settings/api)

В России для этого потребуется ВПН


## MAKE_OWN_DB

#### Создаёт вашу собственную базу данных с фильмами

Запуск осуществляется командой:

`python3 make_own_db.py`

Для работы скрипта вам потребуется ключ API, о том, как его получить, смотрите в разделе HELLO_API_TMDB.

После запуска скрипт запрашивает у пользователя API-ключ, если он не будет введён, пользователь увидит сообщение `Invalid api key`, и скрипт прекратит работу.

Когда ключ введён, в терминал выводится сообщение `please, wait, this operation may take smth like 15-20 minutes`, после чего начинается создание базы данных. Установленное количество фильмов в БД - тысяча

На сайт делается запрос о каждом фильме, номер которого лежит в пределах от 0 до 1000. В случае возникновения ошибки 404 (фильма с таким номером нет на сайте), скрипт продолжает работу, при других HTTP-ошибках работа прерывается, ошибка выводится в терминал. При успешном запросе данные о фильме добавляются в соответствующий список, а в терминал выводится прогресс выполнения в процентах.

![Screenshot from 2024-12-10 15-36-44](https://github.com/user-attachments/assets/d16a497e-5181-4dd6-9d25-7ae25a185b5d)

После завершения загрузки фильмов, скрипт создаёт/открывает файл `MyFilmDB.json` в кодировке utc-8, и записывает в него вашу БД с  фильмами в формате .json.


## SEARCH_IN_DB

#### Ищет в вашей БД фильм по названию

Запуск осуществляется командой:

`python3 search_in_db.py`

Для работы потребуется БД с фильмами, созданная скриптом make_own_db. 

При запуске пользователю нужно ввести путь до файла с БД, если он не будет указан, скрипт завершит работу, в терминал выведется сообщение: `File not found, sorry...`.

При введении корректного пути к БД, пользователь видит сообщение `Enter film to search for:`, после которого необходимо ввести название фильма, который нужно найти.

Поиск осуществляется сравнением введённого названия с `original_title` каждого фильма в БД. Для сравнения оба названия переводятся в строчные буквы.

Название каждого найденного фильма выводится отдельной строкой в консоль.

Пример работы:

![Screenshot from 2024-12-10 17-22-41](https://github.com/user-attachments/assets/7ab17c63-6c01-4828-8f12-6b47b3ad8739)



## FIND_SIMILAR

#### Ищет в вашей БД фильм по названию

Запуск осуществляется командой:

`python3 find_similar.py`

Для работы потребуется БД с фильмами, созданная скриптом make_own_db. 

При запуске пользователю нужно ввести путь до файла с БД, если он не будет указан, скрипт завершит работу, в терминал выведется сообщение: `File not found, sorry...`.

При введении корректного пути к БД, пользователь видит сообщение `Enter film to search for:`, после которого необходимо ввести название интересующего фильма.

По введённому пользователем названию происходит поиск фильма в БД, если такого нет, в терминал выводится `No such film in FilmsDB` и скрипт завершает работу.

Когда нужный фильм найден, по нему осуществляется составление списка рекомендаций. При составлении рейтинга рекомендаций учитываются следующие параметры: принадлежит ли он вашей коллекции, жанры, оригинальный язык и бюджет. У каждого из этих параметров есть числовой эквивалент: 1000, 500, 300 и 100.

Фильм, введённый пользователем, сравнивается по всем этим параметрам со всеми фильмами в БД. Если фильм из ДБ совпадает с пользовательским по каким-то параметрам, сумма их числовых эквивалентов формирует его рейтинг. Чтобы избежать ситуации, когда в список рекомендаций попадёт фильм, по которому мы ищем, его рейтинг удаляется из списка.

В конце фильмы сортируются по рейтингу, и первые восемь из них формируют список рекомендаций, который построчно выводится в консоль.

![Screenshot from 2024-12-10 18-07-23](https://github.com/user-attachments/assets/f2bbd3aa-2496-4a5f-b4ea-dd8954cab85b)





