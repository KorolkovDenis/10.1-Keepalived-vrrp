# 10.1-Keepalived-vrrp

# Домашнее задание к занятию 10.1 «Keepalived/vrrp»

### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c Шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и вашу фамилию и имя
   - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
   - для корректного добавления скриншотов воспользуйтесь инструкцией ["Как вставить скриншот в шаблон с решением"](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
   - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.

Желаем успехов в выполнении домашнего задания!

---

### Задание 1

Разверните топологию из лекции и выполните установку и настройку сервиса Keepalived. 

```
vrrp_instance test {
state "name_mode"
interface "name_interface"
virtual_router_id "number id"
priority "number priority"
advert_int "number advert"
authentication {
auth_type "auth type"
auth_pass "password"
}
unicast_peer {
"ip address host"
}
virtual_ipaddress {
"ip address host" dev "interface" label "interface":vip
}
}

---

Ответ:

Последовательность выполнения:

Создам две ноды: keepalived и keepalived2. На каждой ноде устанавливаю утилиту keepalived:

sudo apt install keepalived

Создадим и настроим файл конфигурации:

sudo nano /etc/keepalived/keepalived.conf

на master-ноде:

![screen1](https://github.com/KorolkovDenis/10.1-Keepalived-vrrp/blob/main/screenshots/work1/screen1.png)

на slave-ноде:

![screen2](https://github.com/KorolkovDenis/10.1-Keepalived-vrrp/blob/main/screenshots/work1/screen2.png)

На этом скрине видно, что первая нода перешла в состояние master, а вторая нода в состояние backup, в зависимости от обозначенных в конфигурационном файле приоритетов и соответственно видно, что наш виртуальный адрес 192.168.43.100/32 сейчас активен на master-ноде:

![screen3](https://github.com/KorolkovDenis/10.1-Keepalived-vrrp/blob/main/screenshots/work1/screen3.png)

Останавливаю службу на master- ноде – виртуальный адрес на мастере пропадает и запускается на slave – ноде:

![screen4](https://github.com/KorolkovDenis/10.1-Keepalived-vrrp/blob/main/screenshots/work1/screen4.png)


```

*В качестве решения предоставьте:*   
*- рабочую конфигурацию обеих нод, оформленную как блок кода в вашем md-файле;*   
*- скриншоты статуса сервисов, на которых видно, что одна нода перешла в MASTER, а вторая в BACKUP state.*   

## Дополнительные задания со звёздочкой*

Эти задания дополнительные. Их можно не выполнять. На зачёт это не повлияет. Вы можете их выполнить, если хотите глубже разобраться в материале.
 
### Задание 2*

Проведите тестирование работы ноды, когда один из интерфейсов выключен. Для этого:
- добавьте ещё одну виртуальную машину и включите её в сеть;
- на машине установите Wireshark и запустите процесс прослеживания интерфейса;
- запустите процесс ping на виртуальный хост;
- выключите интерфейс на одной ноде (мастер), остановите Wireshark;
- найдите пакеты ICMP, в которых будет отображён процесс изменения MAC-адреса одной ноды на другой. 

 *В качестве решения пришлите скриншот до и после выключения интерфейса из Wireshark.*

 ---
 
 Ответ:

Последовательность выполнения:

![screen1](https://github.com/KorolkovDenis/)


 
 ## Более полная работа, всех моих шагов по ходу выполнения в Google:

[Моя работа по Keepalived](https://docs.google.com/)
