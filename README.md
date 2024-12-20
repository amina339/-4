
# Лабораторная работа 4.

Для решения понадобится установить Docker. Можно это делать как в виртуальной машине с установленным Linux, так и через WSL (главное на линукс подобной системе).
## Пример (не надо его включать в отчет!)
Создадим docker image (образ). Для этого понадобится написать Dockerfile. Создаём пустой текстовый документ, где в первую очередь указываем, на основе какого образа будет работать наш.  
```
FROM ubuntu:latest
```
Далее указываем, что мы хотим запустить. В нашем случае мы обновляем пакетный менеджер и устанавливаем ПО под названием cowsay.
```
RUN apt-get update && apt-get install -y cowsay fortune
```
На этом Dockerfile готов, закрываем и сохраняем его под этим названием. В терминале в папке с этим файлом запускаем команду сборки образа с тегом “cowsay”.
```
docker build -t cowsay .
```
Далее запускаем контейнер на основе созданного образа. При создании контейнера передаём ему запуск приложения “cowsay”, которое находится в папке /usr/games и передаём приложению команду "Moo".
```
docker run cowsay /usr/games/cowsay "Moo"
```
Наслаждаемся результатом.  

Далее можем подключиться запустить контейнер и  подключиться к нему напрямую командой
```
docker run -it cowsay
```
И уже напрямую в терминале контейнера запустить команду
```
/usr/games/cowsay "Moo"
```
Проверим запущенные контейнеры у вас на машине командой
```
docker ps
```
Особенность контейнеризации заключается в том, что рекомендуется под один сервис запускать один контейнер. Также, когда сервис отработал, контейнер автоматически заканчивает свою работу. Поскольку своё предназначение данный контейнер выполнил - вы не увидите его в выводе команды.  
Но в случае, если контейнер был запущен с флагом -it – он ожидает ручных команд и не будет отключаться самостоятельно.  

## Задание:  
Запустить в контейнере приложение “aafire”. Обратите внимание, что оно бесконечное и контейнер не будет автоматически отключаться.  
Приложить скриншот в процессе работы контейнера.  

Далее в рамках лабораторной работы необходимо самостоятельно настроить сеть между двумя контейнерами, также как в предыдущей работе вы настраивали связь между двумя виртуальными машинами.  

Для проверки сети между контейнерами вам потребуется утилита ping. Поскольку контейнеры очень маленькие и в них нет ничего лишнего (по сравнению с виртуальными машинами) - ping там не установлен. В вашем образе нужно будет установить пакет с этой утилитой, помимо aafire.  

Далее запустите два контейнера с aafire и оставьте их в работающем состоянии.  
Откройте ещё одно окно терминала и создайте сеть при помощи команды 
```
docker network create myNetwork
```
После этого нужно будет подключить контейнеры к вашей сети. Названия контейнеров можно увидеть при выводе списка действующих контейнеров у вас на машине.
```
docker network connect myNetwork mycontainer1
docker network connect myNetwork mycontainer2
```
Теперь при помощи следующей команды вы можете увидеть настройки созданной вами сети.
```
docker network inspect myNetwork
```
Далее вам нужно самостоятельно протестировать соединение между контейнерами утилитой ping и приложить скриншот.

### Как успешно сдать работу?

Создать свой репозиторий из шаблона этого. Как это делается - "Use this template" -> "Create a new repository" и сделайте его public. 

Находясь уже в своем репозитории - создайте новый файл формата .md и там оформляйте отчет. В отчете опишите все шаги которые вы делали, чтобы получить финальный результат работы.

Что вам нужно знать, чтобы успешно защитить работу:

Как создавать и управлять - докерфайлом (команды, оптимизация), образами (создание, запуск, принцип работы), контейнерами (запуск, отслеживание, объединение); виртуализация и контейнеризация. 

## Источники

[Источник где можно найти все](https://google.com)


# Лабораторная работа

Для решения понадобится виртуальная машина с установленным Linux (если ваша основная ОС уже не Linux)
## Пример (не надо его включать в отчет!)
1. Создайте файл hello.txt
```
 touch hello.txt
```
2. В терминале введите следующую команду, чтобы открыть файл конфигураций (настроек)
```
 crontab -e
```
3. Попав внутрь, введите следующую строку. Она создаст сценарий, по которому каждую минуту в файл hello.txt будет вводиться строка "New line". Сохраните изменения и вернитесь обратно в терминал
```
 * * * * * echo "New line" >> hello.txt
```
4. Теперь файл обновляется каждую минуту, результат выглядит так

     ![image]

     То есть мы создали планировщик, по которому выполняется запуск определенных скриптов и задач в нужное время с заданной регулярностью
## Задание 
Создайте такой сценарий планировщика, чтобы каждый будний день с 9:00 до 17:00 каждые 2 часа в какой-то определенный файл добавлялась новая строка с временем обновления файла. 

Далее в рамках лабораторной работы выведите данные этого файла в терминал в интерактивном режиме (то есть так, чтобы было видно добавление новой строки).
## Как успешно сдать работу?
Создать свой репозиторий из шаблона этого. Как это делается - "Use this template" -> "Create a new repository" и сделайте его public.

Находясь уже в своем репозитории - создайте новый файл формата .md и там оформляйте отчет. В отчете опишите все шаги которые вы делали, чтобы получить финальный результат работы.

Что вам нужно знать, чтобы успешно защитить работу:
- что такое Cron
- как записывать расписание и какие есть для этого переменные
- что такое уведомления и журналирование
- основные команды для работы с Cron
- отличие Cron от At
