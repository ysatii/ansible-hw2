# Домашнее задание к занятию 2 «Работа с Playbook»

## Подготовка к выполнению

1. * Необязательно. Изучите, что такое [ClickHouse](https://www.youtube.com/watch?v=fjTNS2zkeBs) и [Vector](https://www.youtube.com/watch?v=CgEhyffisLY).
2. Создайте свой публичный репозиторий на GitHub с произвольным именем или используйте старый.
3. Скачайте [Playbook](./playbook/) из репозитория с домашним заданием и перенесите его в свой репозиторий.
4. Подготовьте хосты в соответствии с группами из предподготовленного playbook.

## Основная часть

Задание  1.  
  Подготовьте свой inventory-файл `prod.yml`.  

Решение 1.  
листинг prod.yml
```
 GNU nano 4.8                          /home/lamer/Рабочий стол/ansible-hw2/playbook/inventory/prod.yml                                    
clickhouse:
  hosts:
    clickhouse-01:
      ansible_host: 158.160.141.195
      ansible_connection: ssh
      ansible_user: lamer
      ansible_ssh_private_key_file: ssh_env/id_rsa_insecure_clickhouse-01

vector:
  hosts:
    clickhouse-02:
      ansible_host: 158.160.164.93
      ansible_connection: ssh
      ansible_user: lamer
      ansible_ssh_private_key_file: ssh_env/id_rsa_insecure_clickhouse-02
```

2. Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает [vector](https://vector.dev). Конфигурация vector должна деплоиться через template файл jinja2. От вас не требуется использовать все возможности шаблонизатора, просто вставьте стандартный конфиг в template файл. Информация по шаблонам по [ссылке](https://www.dmosk.ru/instruktions.php?object=ansible-nginx-install). не забудьте сделать handler на перезапуск vector в случае изменения конфигурации!
[ссылка на переделанный site.yml](https://github.com/ysatii/ansible-hw2/blob/main/playbook/site.yml)  
[обработчик роли  ](https://github.com/ysatii/ansible-hw2/blob/main/playbook/roles/vector/handlers/main.yml)
[Шаблон конфигурации роли](https://github.com/ysatii/ansible-hw2/blob/main/playbook/roles/vector/templates/vector.toml.j2)
[настройки и выходные директории](https://github.com/ysatii/ansible-hw2/blob/main/playbook/roles/vector/tasks/main.yml)

3. При создании tasks рекомендую использовать модули: `get_url`, `template`, `unarchive`, `file`.
4. Tasks должны: скачать дистрибутив нужной версии, выполнить распаковку в выбранную директорию, установить vector.
5. Запустите `ansible-lint site.yml` и исправьте ошибки, если они есть.
 ![рис 1](https://github.com/ysatii/ansible-hw2/blob/main/img/img_ansble1.jpg)  
 ![рис 2](https://github.com/ysatii/ansible-hw2/blob/main/img/img_ansble2.jpg)
 ![рис 3](https://github.com/ysatii/ansible-hw2/blob/main/img/img_ansble3.jpg)
 ![рис 4](https://github.com/ysatii/ansible-hw2/blob/main/img/img_ansble4.jpg)

Ошибок не обнаружено!  

6. Попробуйте запустить playbook на этом окружении с флагом `--check`.
 ![рис 5](https://github.com/ysatii/ansible-hw2/blob/main/img/img_ansble5.jpg)

7. Запустите playbook на `prod.yml` окружении с флагом `--diff`. Убедитесь, что изменения на системе произведены.
 ![рис 6  ](https://github.com/ysatii/ansible-hw2/blob/main/img/img_ansble6.jpg)


8. Повторно запустите playbook с флагом `--diff` и убедитесь, что playbook идемпотентен.
 ![рис 7](https://github.com/ysatii/ansible-hw2/blob/main/img/img_ansble7.jpg)

9. Подготовьте README.md-файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги. Пример качественной документации ansible playbook по [ссылке](https://github.com/opensearch-project/ansible-playbook). Так же приложите скриншоты выполнения заданий №5-8 
[инструкция](https://github.com/ysatii/ansible-hw2/blob/main/playbook/README.md)

10. Готовый playbook выложите в свой репозиторий, поставьте тег `08-ansible-02-playbook` на фиксирующий коммит, в ответ предоставьте ссылку на него.

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.

---
