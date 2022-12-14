# Документация

### Оглавление
+ [Linux](https://github.com/codesshaman/documentation/#Linux "Linux")
  - [Способы открытия файлов](https://github.com/codesshaman/documentation/#Notes "Notes")
  - [Поиск файлов в системе](https://github.com/codesshaman/documentation/#Find "Find")
  - [Проверить свободные порты](https://github.com/codesshaman/documentation/#Ports "Ports")
  - [Вставка и замена текста](https://github.com/codesshaman/documentation/#Sed "Sed")
  - [Информация о пользователях](https://github.com/codesshaman/documentation/#AboutUsers "AboutUsers")
  - [Терминальные сессии tmux](https://github.com/codesshaman/documentation/#Tmux "Tmux")
  - [Docker](https://github.com/codesshaman/documentation/#Docker "Docker")
    * [Чистый Docker](https://github.com/codesshaman/documentation/#Docker "Docker")
    * [Docker compose](https://github.com/codesshaman/documentation/#Docker-compose "Docker-compose")
    * [Makefile для docker-compose](https://github.com/codesshaman/documentation/#ComposeMakefile "ComposeMakefile")
    * [Docker swarm](https://github.com/codesshaman/documentation/#Docker-swarm "Docker-swarm")
  - [Самоподписные сертификаты mkcert](https://github.com/codesshaman/documentation/#Mkcert "Mkcert")
  - [Логирование](https://github.com/codesshaman/documentation/#Logs "Logs")
  - [Просмотр логов lnav](https://github.com/codesshaman/documentation/#Lnav "Lnav")
+ [Оглавление](https://github.com/codesshaman/documentation/#Оглавление "Оглавление")
+ [Инструкции](https://github.com/codesshaman/documentation/#Инструкции "Инструкции")

***

### Linux
> Утиллиты linux

### Notes
+ [Оглавление](https://github.com/codesshaman/documentation/#Оглавление "Оглавление")
> Блокноты, просмотрщики и т.д.

``nano имя_файла`` - блокнот, аналоги - vi, vim<br>
``cat имя_файла`` - простой вывод в консоль<br>
``less имя_файла`` - листалка (выход на q)<br>
``tail -f имя_файла`` - вывод последних 10 строк с обновлением данных<br>
``tail -n 3 имя_файла`` - вывод последних 3 строк с обновлением данных<br>
``tail -f -s 5 /var/log/syslog`` - просмотр логов с обновлением каждые 5 секунд<br>
``tail -f -s 50 /var/log/syslog | grep err`` - сортировка с выводом только ошибок<br> 
***
### Find
+ [Оглавление](https://github.com/codesshaman/documentation/#Оглавление "Оглавление")
> Поиск файлов в системе

``find directory-to-search criteria action`` - общая маска команды<br>
``find . -name "s.txt"`` - поиск в текущей директории<br>
``find / -name "s.txt"`` - поиск в корневой директории<br>
``find / -iname "s.txt"`` - убрать чувствительность к регистру<br>
``find . -name "*.txt"`` - поиск всех файлов с конкретным расширением<br>
Поиск по типу файла<br>
Критерий -type позволяет искать файлы по типу, которые бывают следующих видов:<br>
``f`` – простые файлы;<br>
``d`` – каталоги;<br>
``l`` – символические ссылки;<br>
``b`` – блочные устройства (dev);<br>
``c`` – символьные устройства (dev);<br>
``p`` – именованные каналы;<br>
``s`` – сокеты;<br>
``find . -type d`` - вывод всех каталогов в текущей директории<br>
``find . -size +1G`` - поиск файлов более 1 гигабайта<br>
Единицы измерения файлов:<br>
``c`` — Байт<br>
``k`` — Кбайт<br>
``M`` — Мбайт<br>
``G`` — Гбайт<br>
``find . -empty`` - найти только пустые файлы и каталоги<br>
``find . -cmin -60`` - найти по времени изменения (последние 60 минут)<br>
``find /home -perm 777`` - поиск по набору разрешений<br>
Операторы<br>
Для объединения нескольких критериев в одну команду поиска можно применять операторы:<br>
-``and``<br>
-``or``<br>
-``not``<br>
Например, чтобы найти файлы размером более 1 Гбайта пользователя tisha необходимо ввести следующую команду:<br>
``find /home  -user tisha  -and  -size +1G  2>/dev/null``<br>
Если файлы могут принадлежать не только пользователю tisha, но и пользователю pokeristo, а также быть размером более 1 Гбайта.<br>
``find /home \( -user pokeristo -or -user tisha \)  -and  -size +1G  2>/dev/null``<br>
Действия<br>
К команде find можно добавить действия, которые будут произведены с результатами поиска.<br>
-``delete`` — Удаляет соответствующие результатам поиска файлы<br>
-``ls`` — Вывод более подробных результатов поиска с:<br>
Размерами файлов.<br>
Количеством inode.<br>
-``print`` Стоит по умолчанию, если не указать другое действие. Показывает полный путь к найденным файлам.<br>
-``exec`` Выполняет указанную команду в каждой строке результатов поиска.<br>
``find . -empty -delete`` - удалить все пустые директории<br>
``find . -empty -exec rm -r {} \;`` - удалить все пустые директории командой rm<br>
``find . -name "*.jpg" -exec cp {} /images \;`` - перенести все jpeg в папку images<br>

Пример: ``find /Users/kgolda/temp/for_git/test_2/.git -type f -name ".DS_*" -delete`` - найти и удалить все файлы .DS_*
***
### Ports
+ [Оглавление](https://github.com/codesshaman/documentation/#Оглавление "Оглавление")
> Утиллиты для проверки портов

#### netstat
``dnf install net-tools``</br>
``netstat -pnltu``</br>
``netstat -pnltu | grep -i "22"``</br>
``netstat -tulpn | grep LISTEN``</br>
#### ss
``ss -lntu``</br>
``ss -lntu -p``</br>
#### nmap
``dnf install nmap``</br>
``nmap -n -PN -sT -sU -p- ВашIP``</br>
#### lsof
``lsof -i``</br>
``lsof -i 80``</br>
***
### Sed
+ [Оглавление](https://github.com/codesshaman/documentation/#Оглавление "Оглавление")
> Удаление, вставка и замена строк в файлах

``sed -i '3d' filename.txt`` - удаление третьей строки в файле</br>
``sed -i '$d' filename.txt`` - удаление последней строки в файле</br>
``sed -i '/^$/d' filename.txt`` - удаление всех пустых строк в файле</br>
``sed -i '/TOKEN_PURCHASE=/d' filename.txt`` - удаление строки по содержимому</br>
``sed -i -e '5,10d;13d' filename.txt`` - удаление с 5 по 10 и 13 строк</br>
``sed -i '1i # comment\n' filename.txt`` - комментарий с переносом в первую строку файла</br>
``sed -i 's/FOO/BAR/g' filename.txt`` - замена ВСЕХ foo на bar в файле</br>
``sed -i '0,/FOO/s/FOO/BAR/' filename.txt`` - замена первого foo на bar</br>
``sed -i '3i\Это новая строка' filename.txt`` - вставка строки после третьей</br>

Дополнительно:

``grep -n 'TEXT' filename.txt | cut -d: -f1`` - вывод номера строки по тексту
***
### AboutUsers
+ [Оглавление](https://github.com/codesshaman/documentation/#Оглавление "Оглавление")
> Просмотр информации о пользователях и сессиях

``who`` - кто на данный момент находится в системе</br>
``last`` - когда и насколько пользователь заходил в систему</br>
``last <username>``  - информация по конкретному пользователю</br>
``lastlog`` - все пользователи с датами последнего входа</br>
***
### Tmux
+ [Оглавление](https://github.com/codesshaman/documentation/#Оглавление "Оглавление")
> Удобное использование терминального пространства при помощи tmux

``tmux new-session -s test`` - создать сессию с названием test</br>
``Ctrl+b %`` - разбить терминал по горизонтали</br>
``Ctrl+b "`` - разбить терминал по вертикали</br>
``Ctrl+b x`` - закрыть окно терминала</br>
``Ctrl+b d`` - отключиться от рабочего терминала</br>
``Ctrl+b c`` - создать новое окно</br>
``Ctrl+b n`` - переключиться на следующее окно</br>
``Ctrl+b p`` - переключиться на предыдущее окно</br>
``tmux attach -t test`` - присоединиться к сессии с названием test</br>
``tmux ls`` - список сессий</br>
``tmux kill-session -t test`` - стереть сессию</br>
``tmux source-file ~/.tmux.conf`` - подсунуть конфиг</br>
##### Содержимое конфига для включения мыши и сохранения сессий:
```
set -g mouse on
setw -g xterm-keys on
tmux-session save
tmux-session restore
```
***
### Docker
+ [Оглавление](https://github.com/codesshaman/documentation/#Оглавление "Оглавление")
> Команды чистого докера

### Docker-compose
+ [Оглавление](https://github.com/codesshaman/documentation/#Оглавление "Оглавление")
> Команды docker-compose

### ComposeMakefile
+ [Оглавление](https://github.com/codesshaman/documentation/#Оглавление "Оглавление")
> Makefile для docker-compose
```
name = docker_configuration
all:
	@printf "Запуск конфигурации ${name}...\n"
	@docker-compose -f ./docker-compose.yml up -d
down:
	@printf "Остановка конфигурации ${name}...\n"
	@docker-compose -f ./docker-compose.yml down
re:
	@printf "Пересборка конфигурации ${name}...\n"
	@docker-compose -f ./docker-compose.yml up -d --build
clean: down
	@printf "Очистка конфигурации ${name}...\n"
	@docker system prune --a
fclean:
	@printf "Полная очистка всех конфигураций docker\n"
#	@docker stop $$(docker ps -qa)
#	@docker system prune --all --force --volumes
#	@docker network prune --force
#	@docker volume prune --force
.PHONY	: all down re clean fclean
```

### Docker-swarm
+ [Оглавление](https://github.com/codesshaman/documentation/#Оглавление "Оглавление")
> Команды docker в режиме роя

***
### Mkcert
+ [Оглавление](https://github.com/codesshaman/documentation/#Оглавление "Оглавление")
> Получение самоподписного сертификата при помощи mkcert

#### Установка:

``sudo apt install -y wget curl libnss3-tools``<br>
``curl -s https://api.github.com/repos/FiloSottile/mkcert/releases/latest| grep browser_download_url | grep linux-amd64 | cut -d '"' -f 4 | wget -qi -``<br>
``mv mkcert-v*-linux-amd64 mkcert``<br>
``chmod a+x mkcert``<br>
``sudo mv mkcert /usr/local/bin/``<br>

#### Проверка:

``mkcert --version``

#### Генерация:

``mkcert localhost``<br>
``mv localhost-key.pem localhost.key``<br>
``mv localhost.pem localhost.crt``<br>
***
### Logs
+ [Оглавление](https://github.com/codesshaman/documentation/#Оглавление "Оглавление")
> Логи linux

Основная папка логов: **/var/log**

Файл лога  |  Назначение
------ | ------
**syslog** | главный системный лог
**auth.log** | все попытки входа на сервер + ip
**dmesg** | лог драйверов
**dpkg.log** | лог менеджера пакетов
**faillog** | лог неудачных попыток входа в систему

[Просматривать в блокнотах](https://github.com/codesshaman/documentation/#Notes "Notes") * 
[Ролик в youtube](https://www.youtube.com/watch?v=p7BNIBFsgPM)
***
### Lnav
+ [Оглавление](https://github.com/codesshaman/documentation/#Оглавление "Оглавление")
> Утиллита для просмотра логов

 ***Установка***<br>
 ``sudo apt install lnav``<br>
 ***Использование***<br>
``sudo lnav`` - просмотр syslog<br>
``sudo lnav /var/log/auth.log /var/log/dpkg.log`` - просмотр нескольких конкретных логов<br>
***
Вы можете создавать свои комбинации!
### Инструкции
+ [Заголовки](https://github.com/AndreyKozhev/Markdown-format#заголовки "Заголовки")
+ [Выделение](https://github.com/AndreyKozhev/Markdown-format#выделение "Выделение")
+ [Списки](https://github.com/AndreyKozhev/Markdown-format#списки "Списки")
+ [Ссылки](https://github.com/AndreyKozhev/Markdown-format#ссылки "Ссылки")
+ [Изображения](https://github.com/AndreyKozhev/Markdown-format#изображения "Изображения")
+ [Блоки кода](https://github.com/AndreyKozhev/Markdown-format#блоки-кода "Блоки кода")
+ [Таблицы](https://github.com/AndreyKozhev/Markdown-format#таблицы "Таблицы")
+ [Цитаты](https://github.com/AndreyKozhev/Markdown-format#цитаты "Цитаты")
+ [Эмодзи](https://github.com/AndreyKozhev/Markdown-format#эмодзи "Эмодзи")
+ [HTML](https://github.com/AndreyKozhev/Markdown-format#html "HTML")
+ [Списки задач](https://github.com/AndreyKozhev/Markdown-format#списки-задач)
+ [Разделительная черта](https://github.com/AndreyKozhev/Markdown-format#%D1%80%D0%B0%D0%B7%D0%B4%D0%B5%D0%BB%D0%B8%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F-%D1%87%D0%B5%D1%80%D1%82%D0%B0)
+ [Блоки Примечание и Предупреждение](https://github.com/AndreyKozhev/Markdown-format#%D0%B1%D0%BB%D0%BE%D0%BA%D0%B8-%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%87%D0%B0%D0%BD%D0%B8%D0%B5-%D0%B8-%D0%BF%D1%80%D0%B5%D0%B4%D1%83%D0%BF%D1%80%D0%B5%D0%B6%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5 "Блоки Примечание и Предупреждение")
+ [Упоминание человека или организации](https://github.com/AndreyKozhev/Markdown-format#%D1%83%D0%BF%D0%BE%D0%BC%D0%B8%D0%BD%D0%B0%D0%BD%D0%B8%D0%B5-%D1%87%D0%B5%D0%BB%D0%BE%D0%B2%D0%B5%D0%BA%D0%B0-%D0%B8%D0%BB%D0%B8-%D0%BE%D1%80%D0%B3%D0%B0%D0%BD%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D0%B8 "Упоминание челове6ка или организации")
