# Домашнее задание к занятию «Защита сети» - Калитвянский Александр SYS-27

### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и ваши фамилию и имя;
   - в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
   - для корректного добавления скриншотов воспользуйтесь инструкцией [«Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.

Желаем успехов в выполнении домашнего задания.

------

### Подготовка к выполнению заданий

1. Подготовка защищаемой системы:

- установите **Suricata**,
- установите **Fail2Ban**.

2. Подготовка системы злоумышленника: установите **nmap** и **thc-hydra** либо скачайте и установите **Kali linux**.

Обе системы должны находится в одной подсети.

------

### Задание 1

Проведите разведку системы и определите, какие сетевые службы запущены на защищаемой системе:

**sudo nmap -sA < ip-адрес >**

**sudo nmap -sT < ip-адрес >**

**sudo nmap -sS < ip-адрес >**

**sudo nmap -sV < ip-адрес >**

По желанию можете поэкспериментировать с опциями: https://nmap.org/man/ru/man-briefoptions.html.


*В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.*  

Suricata мощная система обнаружения вторжений, которая обеспечивает надежную защиту для сетевых сред. Помимо обнаружения и предотвращения вторжений Suricata используется для сбора статистики о сетевой активности, включая количество и тип трафика, источники и назначения трафика, а также для анализа поведения пользователей и приложений:  
![Скриншот 1](https://github.com/akalitvyanskiy/network_protection/blob/main/img/1.png)
![Скриншот 2](https://github.com/akalitvyanskiy/network_protection/blob/main/img/11.png)
![Скриншот 3](https://github.com/akalitvyanskiy/network_protection/blob/main/img/12.png)
![Скриншот 4](https://github.com/akalitvyanskiy/network_protection/blob/main/img/13.png)
![Скриншот 5](https://github.com/akalitvyanskiy/network_protection/blob/main/img/14.png)
![Скриншот 6](https://github.com/akalitvyanskiy/network_protection/blob/main/img/15.png)
![Скриншот 7](https://github.com/akalitvyanskiy/network_protection/blob/main/img/16.png)
![Скриншот 8](https://github.com/akalitvyanskiy/network_protection/blob/main/img/17.png)
![Скриншот 9](https://github.com/akalitvyanskiy/network_protection/blob/main/img/18.png)
![Скриншот 10](https://github.com/akalitvyanskiy/network_protection/blob/main/img/19.png)
![Скриншот 11](https://github.com/akalitvyanskiy/network_protection/blob/main/img/191.png)
![Скриншот 12](https://github.com/akalitvyanskiy/network_protection/blob/main/img/192.png)
![Скриншот 13](https://github.com/akalitvyanskiy/network_protection/blob/main/img/193.png)  

Основной идеей fail2ban является отслеживание логов общих сервисов для выявления ошибок аутентификации. В данном случае атаки по побдбору паролей не было, и соответсвенно ошибок аутентификации выявлено не было. Ниже приведен листинг лога fail2ban.  
![Скриншот 14](https://github.com/akalitvyanskiy/network_protection/blob/main/img/195.png)
![Скриншот 15](https://github.com/akalitvyanskiy/network_protection/blob/main/img/196.png)

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
![Скриншот 16](https://github.com/akalitvyanskiy/network_protection/blob/main/img/2.png)
![Скриншот 17](https://github.com/akalitvyanskiy/network_protection/blob/main/img/21.png)  

В приведенных выше листингов видна работа fail2ban, после обнуружения ряда неудачных попыток авторизации ip адрес 192.168.122.27 был заблокирован. Количество поаыток и временной интервал на который будет блокироваться ip адрес определяется в разделе SSH конфигурационного файла. Администратор может настроить этот параметр самостоятельно исходя из внутренней политики информационной безопасности.  
Suricata в свою очередь зафиксировала сетевую активность на порту 22, используемому службой SSH, что видно в представленном ниже листинге логфайла fast.log.
![Скриншот 18](https://github.com/akalitvyanskiy/network_protection/blob/main/img/22.png)
![Скриншот 19](https://github.com/akalitvyanskiy/network_protection/blob/main/img/23.png)  


