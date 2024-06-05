# Домашнее задание к занятию "`Disaster recovery и Keepalived`" - `Ли Олег`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1


....


`![image](https://github.com/ELK23/disreckeep/assets/67402682/7e417746-4b9c-4fc9-a68a-8c58b591bbb6)
![image](https://github.com/ELK23/disreckeep/assets/67402682/fe5ca4f1-e932-4186-bb12-72a5e8629191)
![image](https://github.com/ELK23/disreckeep/assets/67402682/a6eec204-eb8f-42cd-a2a4-949abd107ec6)


`


---

### Задание 2


```
vrrp_script check_nginx {
  script "/bin/check_nginx.sh"
  interval 3
  weight 1
}

vrrp_script check_file {
  script "/bin/check_file.sh"
  interval 3
  weight 2
}

vrrp_instance VI_1 {
        state MASTER
        interface enp0s3
        virtual_router_id 15
        priority 101
        advert_int 1

        virtual_ipaddress {
              172.156.10.53/24
        }

        track_script {
              check_nginx
              check_file
}
}

#!/bin/bash
if [ ! -f /var/www/html/index.nginx-debian.html ]; then
    exit 1
else
    exit 0
fi


#!/bin/bash
REMOTEHOST=127.0.0.1
REMOTEPORT=80
TIMEOUT=5

(echo ^]; echo quit) | timeout --signal=9 5 telnet $REMOTEHOST $REMOTEPORT > /dev/null 2>&1
TELNET_EXIT_CODE=$?

if [[ $TELNET_EXIT_CODE -ne 0 ]]; then
    nc -w $TIMEOUT -z $REMOTEHOST $REMOTEPORT > /dev/null 2>&1
    NC_EXIT_CODE=$?
fi

if [[ $TELNET_EXIT_CODE -eq 0 ]] || [[ $NC_EXIT_CODE -eq 0 ]]; then
    exit 0
else
    exit 1
fi



vrrp_instance VI_1 {
        state BACKUP
        interface enp0s3
        virtual_router_id 15
        priority 103
        advert_int 1

        virtual_ipaddress {
              172.156.10.53/24
        }

}

```

`![image](https://github.com/ELK23/disreckeep/assets/67402682/ec660959-7a96-4c69-85ea-f1a52639712c)
)
![image](https://github.com/ELK23/disreckeep/assets/67402682/902e70c7-bc0e-45ce-b4ca-44dde370eec8)

`


