## Part 1. Установка ОС

##### **Ubuntu 20.04 Server LTS** установилась
![linux](images/1/1.png)


## Part 2. Создание пользователя

##### Создаём нового пользователя (`sudo adduser new_user_1`) и добавляем его в группу adm (`sudo usermod -aG adm new_user_1`)
![linux](images/2/1.png)
##### Переходим к пользователю - `sudo su new_user_1` и проверяем его группу `groups`
![linux](images/2/2.png)
##### Вывод команды `cat /etc/passwd` 
![linux](images/2/3.png)

## Part 3. Настройка сети ОС

##### Редактирую файл `/etc/hosts` при помощи Vim. И выхожу с сохранением(`:wq`)
![linux](images/3/1.png)
##### Название машины действительно поменялось
![linux](images/3/2.png)

##### Узнаю текущий часовой пояс: `timedatectl`
![linux](images/3/3.png)
##### Команда `timedatectl list-timezones` выводит список длинных названий часовых поясов.
![linux](images/3/4.png)
##### Находим Москву. Часовой пояс Москвы записан, как `Europe/Moscow`
#####  Меняем часовой пояс: `sudo timedatectl set-timezone Europe/Moscow` и проверяем изменения
![linux](images/3/5.png)

##### Вывести названия сетевых интерфейсов с помощью консольной команды.
##### Вывожу названия сетевых интерфейсов
![linux](images/3/6.png)
- Объяснение наличия lo в списке с сетевыми интерфейсами. 

  lo (loopback device) – виртуальный интерфейс, присутствующий по
умолчанию в любом Linux. Он используется для отладки сетевых программ
и запуска серверных приложений на локальной машине. С этим интерфейсом
всегда связан адрес 127.0.0.1. У него есть dns-имя – localhost.
##### Используя консольную команду получить ip адрес устройства, на котором вы работаете, от DHCP сервера.
##### `hostname -I` - вывод ip-адреса
![linux](images/3/7.png)
##### DHCP (англ. Dynamic Host Configuration Protocol — протокол динамической настройки узла) — сетевой
протокол, позволяющий компьютерам автоматически получать IP-адрес
и другие параметры, необходимые для работы в сети.
##### `curl ifconfig.me` - внешний ip - адрес
![linux](images/3/8.png)
##### `ip route` - внутренний ip - адрес
![linux](images/3/9.png)
##### Задать статичные (заданные вручную, а не полученные от DHCP сервера) настройки ip, gw, dns (использовать публичный DNS серверы, например 1.1.1.1 или 8.8.8.8).
##### Перезагрузить виртуальную машину. Убедиться, что статичные сетевые настройки (ip, gw, dns) соответствуют заданным в предыдущем пункте.
##### Открываем файл 00-installer-config.yaml - `sudo vim /etc/netplan/00-installer-config.yaml` и устанавливаем значение dhcp4 равное no.
![linux](images/3/10.png)
##### Чтобы применить внесенные изменения, выполнием команду: `sudo netplan apply`
##### Проверяем получили ли мы статичный ip - `ip route`
![linux](images/3/11.png)
##### Перезагружаем виртуальную машину и проверяем снова
![linux](images/3/12.png)
- В отчёте опишите, что сделали для выполнения всех семи пунктов (можно как текстом, так и скриншотами).
- Успешно пропинговать удаленные хосты 1.1.1.1 и ya.ru и вставить в отчёт скрин с выводом команды. В выводе команды должна быть фраза "0% packet loss".
##### Пропингуем удаленные хосты 1.1.1.1 и ya.ru
![linux](images/3/13.png)
![linux](images/3/14.png)

## Part 4. Обновление ОС

![linux](images/4/1.png)

## Part 5. Использование команды **sudo**

Команда sudo ( substitute user and do, подменить пользователя и выполнить )
позволяет строго определенным пользователям выполнять указанные программы с
- административными привилегиями без ввода пароля суперпользователя root.
##### `sudo usermod -aG sudo new_user_1` - разрешил пользователю выполнять команду sudo.
##### `sudo su new_user_1` - переключился на этого пользователя
##### в vim изменил название на `part5`
##### перезагрузил виртуальную машину и убедился в изменениях
![linux](images/5/1.png)

## Part 6. Установка и настройка службы времени

- Время, часовой пояс, в котором сейчас находимся.
![linux](images/6/1.png)

##### Устанавливаем systemd-timesyncd - `sudo apt install systemd-timesyncd`
##### Открываем /etc/systemd/timesyncd.conf - `sudo vim /etc/systemd/timesyncd.conf` и задаем FallbackNTP равный `ntp.sbercloud.ru`
##### systemctl restart systemd-timesyncd - перезапускаем
##### `systemctl status systemd-timesyncd.service` - проверяем запущена ли служба `systemd-timesyncd`
![linux](images/6/2.png)
- Проверяем статус синхронизации часов
![linux](images/6/3.png)

## Part 7. Установка и использование текстовых редакторов

- `sudo apt install joe` - устанавливаем Joe. Vim и nano уже установлены.
### VIM
- `vim test_vim.txt` - создаю и открываю файл.
![linux](images/7/vim.png)
- Для выхода с сохранением: `(esc):wq`

### Nano
- `nano test_nano.txt` - создаю и открываю файл.
  ![linux](images/7/nano.png)
- Нажимаю `control + X`, чтобы выйти. `Y` - нажимаю yes, чтобы выйти с сохранением.  `enter` - подтверждаю название файла.

### joe
- `joe test_joe.txt` - создаю и открываю файл.
  ![linux](images/7/joe.png)
- Нажимаю `control + k + q`, чтобы выйти. `y` - нажимаю yes, чтобы выйти с сохранением.


### VIM
- `vim test_vim.txt` - открываю файл.
  ![linux](images/7/vim2.png)
- Для выхода без сохранения: `(esc):q!`
- ![linux](images/7/vim3.png)

### Nano
- `nano test_nano.txt` - открываю файл.
  ![linux](images/7/nano2.png)
- Нажимаю `control + X`, чтобы выйти. `n` - нажимаю no, чтобы выйти без сохранения.  `enter` - подтверждаю название файла.
- ![linux](images/7/nano3.png)

### joe
- `joe test_joe.txt` - открываю файл.
  ![linux](images/7/joe2.png)
- Нажимаю `control + k + q`, чтобы выйти. `n` - нажимаю no, чтобы выйти без сохранения.
- ![linux](images/7/joe3.png)



### VIM
- `vim test_vim.txt` - открываю файл.
  ![linux](images/7/vim4.png)
- с помощью `(esc):s/` можно искать слова
- и заменять их. заменяю dir на qwerty: `(esc):s/dir/qwerty/g`
- флаг g нужен для замены во всём файле


### Nano
- `nano test_nano.txt` - открываю файл.
  ![linux](images/7/nano4.png)
- Нажимаю `control + \`, чтобы войти в режим замены. Ввожу слово, которое нужно заменить. Ввожу слово, на которое нужно заменить. нажимаю yes.

### joe
- `joe test_joe.txt` - открываю файл.
  ![linux](images/7/joe4.png)
- Нажимаю `control + k + f`, чтобы войти в режим поиска. Ввожу слово, которое нужно заменить. Выбираю режим r(replace). Ввожу слово, на которое нужно заменить. нажимаю yes.

## Part 8. Установка и базовая настройка сервиса **SSHD**

##### `sudo apt-get install openssh-server` - Установка OpenSSH в Ubuntu
- `sudo systemctl enable sshd` - Добавляю автостарт службы при загрузке системы.
  ![linux](images/8/1.png)

- Все настройки сервера SSH хранятся в конфигурационном файле sshd_config, который находится в папке /etc/ssh. Перед тем как вносить изменения в этот конфигурационный файл
сделаем его резервную копию:`sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.factory-defaults`
- Теперь открываем этот файл через Vim
 ![linux](images/8/2.png)
- Находим строку с надписью `#Port` и меняем на 2022. Также нужно удалить решётку, чтобы раскомментировать строку. Далее выходим с сохранением.
- `ps -A(-e)` - флаги A и e выбирают все процессы
  ![linux](images/8/3.png)
-Команда ps(process status) является очень гибким инструментом для определения работающих в системе программ и оценки используемых ими ресурсов. Она выводит статистику и 
информацию о состоянии процессов в системе, в том числе ИД процесса или нити, объем выполняемого ввода-вывода и используемый объем ресурсов процессора и памяти.
- `sudo systemctl restart ssh` - перезапускаем службу SSH
  
![linux](images/8/4.png)
- запускаю Firewall
- разрешил доступ к новому порту ssh: `sudo ufw allow 2222`
##### Перезапустил систему
- вывод команды `netstat -tan`
![linux](images/8/5.png)
##### Объяснение ключей:
- t - показывает только TCP порты
- a - Отображение всех подключений и ожидающих портов.
- n - Отображение адресов и номеров портов в числовом формате.
##### Объяснение столбцов:
- Proto - протокол сокета
- Recv-Q - количество полученных пакетов в очереди
- Send-Q - количество отправленных пакетов в очереди
- Local Address - адрес и номер порта локального конца сокета
- Foreign Address - адрес и номер порта удаленного конца сокета
- State - состояние сокета
- значение 0.0.0.0 означает, что порт прослушивается на всех "сетевых интерфейсах" (т.е. на вашем компьютере, модеме (модемах) и сетевой карте (картах)).


## Part 9. Установка и использование утилит **top**, **htop**

##### запустил утилиты top и htop.
![linux](images/9/1.png)
  - uptime - 5 min
  - количество авторизованных пользователей - 1 
  - общую загрузку системы - 0.00, 0.05, 0.03
  - общее количество процессов - 96 total, 1 running, 95 sleeping, 0 stopped, 0 zombie
  - загрузку cpu - 0.0 us, 0.0 sy, 0.0 ni, 100.0 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st
  - загрузку памяти - 1983.4 total, 1441.0 free, 149.6 used, 392.8 buff/cache
  - pid процесса занимающего больше всего памяти - 721
    ![linux](images/9/2.png)
  - pid процесса, занимающего больше всего процессорного времени - 1160
    ![linux](images/9/3.png)
- Вывод команды htop:
  - Сортировка по PID
    ![linux](images/9/PID.png)

  -Сортировка по PERCENT_CPU
   ![linux](images/9/PERCENT_CPU.png)

  -Сортировка по PERCENT_MEM
    ![linux](images/9/PERCENT_MEM.png)

  -Сортировка по TIME
    ![linux](images/9/TIME.png)

  - отфильтрованному для процесса sshd
    ![linux](images/9/sshd.png)
  
  - с процессом syslog, найденным, используя поиск
    ![linux](images/9/syslog.png)
  
  - с добавленным выводом hostname, clock и uptime
    ![linux](images/9/4.png)

  
## Part 10. Использование утилиты **fdisk**

 ![linux](images/10/1.png)
- название жесткого диска - /dev/sda 
- размер - 15 Гб
- количество секторов - 31457280 
- размер swap - 1.9 Гб
  ![linux](images/10/2.png)
- 
## Part 11. Использование утилиты **df**

##### Команда df.
![linux](images/11/1.png)
- В отчёте написать для корневого раздела (/):
  - размер раздела - 10218772
  - размер занятого пространства - 4829616
  - размер свободного пространства - 4848484
  - процент использования - 50%
- единица измерения в выводе - килобайт

#####  Команда df -Th.
 ![linux](images/11/2.png)
- В отчёте написать для корневого раздела (/):
    - размер раздела - 9.8 Гб
    - размер занятого пространства - 4.7 Гб
    - размер свободного пространства - 4.7 Гб
    - процент использования - 50%
- Тип файловой системы для раздела - ext4

## Part 12. Использование утилиты **du**

- Запустил команду du
  ![linux](images/12/1.png)
- Вывод размера папок /home, /var, /var/log (в байтах, в человекочитаемом виде)
  ![linux](images/12/2.png)
- Вывод размера всего содержимого в /var/log (не общее, а каждого вложенного элемента, используя *)
  ![linux](images/12/3.png)

## Part 13. Установка и использование утилиты **ncdu**

##### Установил утилиту ncdu.
![linux](images/13/1.png)

- Просканируем всю файловую систему: `ncdu -x /`
 ![linux](images/13/2.png)
тут видно размеры /home и /var
- Просканируем папку /var
![linux](images/13/3.png)
тут видно размер /var/log

## Part 14. Работа с системными журналами

##### Открыл для просмотра:
##### 1. sudo cat /var/log/dmesg
![linux](images/14/1.png)
##### 2. sudo cat /var/log/syslog
![linux](images/14/2.png)
##### 3. sudo cat /var/log/auth.log
![linux](images/14/3.png)

- Время последней успешной авторизации, имя пользователя и метод входа в систему: `sudo cat /var/log/auth.log | grep login`
  ![linux](images/14/4.png)
  - Время - 10 Апреля 17:25:14
  - Имя пользователя - dirgekas
  - Метод входа в систему - systemd-logind 
- Перезапустил службу SSHd.
![linux](images/14/5.png)
- Вставил в отчёт скрин с сообщением о рестарте службы (искал в логах): `grep restart /var/log/auth.log`
![linux](images/14/6.png)

## Part 15. Использование планировщика заданий **CRON**

##### Используя планировщик заданий, запустите команду uptime через каждые 2 минуты.
 - открываю файл через `crontab -e` и задаю запуск команды uptime через каждые 2 минуты.
![linux](images/15/1.png)
 - Найти в системных журналах строчки (минимум две в заданном временном диапазоне) о выполнении.
   ![linux](images/15/3.png)
 - Вывести на экран список текущих заданий для CRON.
   ![linux](images/15/4.png)

##### Удалил все задания из планировщика заданий.

![linux](images/15/5.png)



💡 [Нажми тут](https://forms.yandex.ru/cloud/641817c002848f26a078c4a6/), **чтобы поделиться с нами обратной связью на этот проек**т. Это анонимно и поможет команде Педаго сделать твоё обучение лучше.
