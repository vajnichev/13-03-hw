# Домашнее задание к занятию «Защита сети» - Важничев Георгий

### Задание 1

Проведите разведку системы и определите, какие сетевые службы запущены на защищаемой системе:

**sudo nmap -sA < ip-адрес >**

**sudo nmap -sT < ip-адрес >**

**sudo nmap -sS < ip-адрес >**

**sudo nmap -sV < ip-адрес >**

По желанию можете поэкспериментировать с опциями: https://nmap.org/man/ru/man-briefoptions.html.


*В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.*


### Подготовка к выполнению заданий

1. Подготовка защищаемой системы:

- установите **Suricata**,
- установите **Fail2Ban**.

2. Подготовка системы злоумышленника: установите **nmap** и **thc-hydra** либо скачайте и установите **Kali linux**.

Обе системы должны находится в одной подсети.

#### Защищаемая система - Debian - enp0s8 - 192.168.56.105
![png](https://github.com/vajnichev/13-03-hw/blob/main/img/13.3.2.png)
#### Система злоумышленника - Kali Linux - eth1 - 192.168.56.103
![png](https://github.com/vajnichev/13-03-hw/blob/main/img/13.3.1.png)

### Ответ:


Suricata сработал везде, кроме первого запроса -sA. В остальных же случаях лог Suricata выдает, что происходило подозрительное скарирование и классификация идет как "Потенциально опасный трафик" и "Возможна утечка информации".

Fail2Ban во всех случаях молчал.
![png](https://github.com/vajnichev/13-03-hw/blob/main/img/13.3.3.png)
![png](https://github.com/vajnichev/13-03-hw/blob/main/img/13.3.4.png)
![png](https://github.com/vajnichev/13-03-hw/blob/main/img/13.3.5.png)
![png](https://github.com/vajnichev/13-03-hw/blob/main/img/13.3.6.png)
![png](https://github.com/vajnichev/13-03-hw/blob/main/img/13.3.7.png)
![png](https://github.com/vajnichev/13-03-hw/blob/main/img/13.3.8.png)
![png](https://github.com/vajnichev/13-03-hw/blob/main/img/13.3.9.png)
![png](https://github.com/vajnichev/13-03-hw/blob/main/img/13.3.10.png)
![png](https://github.com/vajnichev/13-03-hw/blob/main/img/13.3.11.png)
![png](https://github.com/vajnichev/13-03-hw/blob/main/img/13.3.12.png)
![png](https://github.com/vajnichev/13-03-hw/blob/main/img/13.3.13.png)


------

### Задание 2

Проведите атаку на подбор пароля для службы SSH:

**hydra -L users.txt -P pass.txt < ip-адрес > ssh**

1. Настройка **hydra**: 
 
 - создайте два файла: **users.txt** и **pass.txt**;
 - в каждой строчке первого файла должны быть имена пользователей, второго — пароли. В нашем случае это могут быть случайные строки, но ради эксперимента можете добавить имя и пароль существующего пользователя.

Дополнительная информация по **hydra**: https://kali.tools/?p=1847.

2. Включение защиты SSH для Fail2Ban:

-  открыть файл /etc/fail2ban/jail.conf,
-  найти секцию **ssh**,
-  установить **enabled**  в **true**.

Дополнительная информация по **Fail2Ban**:https://putty.org.ru/articles/fail2ban-ssh.html.



*В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.*
### Ответ:

Пароль не был подобран, так как атакующая машина попала в бан. 
Получаем ошибку, что нет возможности соединиться с атакуемым хостом, так как в соединении отказано.
![png](https://github.com/vajnichev/13-03-hw/blob/main/img/13.3.15.png)


#### События Suricata 
![png](https://github.com/vajnichev/13-03-hw/blob/main/img/13.3.14.png)
#### События Fail2Ban
![png](https://github.com/vajnichev/13-03-hw/blob/main/img/13.3.16.png)
