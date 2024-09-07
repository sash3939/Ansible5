# Домашнее задание к занятию 5 «Тестирование roles»

## Подготовка к выполнению

1. Установите molecule и его драйвера: `pip3 install "molecule molecule_docker molecule_podman`.
2. Выполните `docker pull aragast/netology:latest` —  это образ с podman, tox и несколькими пайтонами (3.7 и 3.9) внутри.

## Основная часть

Ваша цель — настроить тестирование ваших ролей. 

Задача — сделать сценарии тестирования для vector. 

Ожидаемый результат — все сценарии успешно проходят тестирование ролей.

### Molecule

1. Запустите  `molecule test -s ubuntu_xenial` (или с любым другим сценарием, не имеет значения) внутри корневой директории clickhouse-role, посмотрите на вывод команды. Данная команда может отработать с ошибками или не отработать вовсе, это нормально. Наша цель - посмотреть как другие в реальном мире используют молекулу И из чего может состоять сценарий тестирования.

<img width="671" alt="Screen1" src="https://github.com/user-attachments/assets/8b131394-2190-407a-8e3d-11029dc8bf1f">

2. Перейдите в каталог с ролью vector-role и создайте сценарий тестирования по умолчанию при помощи `molecule init scenario --driver-name docker`.

<img width="598" alt="Screen2" src="https://github.com/user-attachments/assets/3866f742-f3dc-412d-a811-6cd16827880a">
 
3. Добавьте несколько разных дистрибутивов (oraclelinux:8, ubuntu:latest) для инстансов и протестируйте роль, исправьте найденные ошибки, если они есть.

<img width="469" alt="Screen3" src="https://github.com/user-attachments/assets/4dc467bd-96c7-42a9-be23-efc266f064ff">

<img width="619" alt="Screen4" src="https://github.com/user-attachments/assets/5d4e0a0b-74d2-4ccc-9182-af22f5968738">

<img width="612" alt="Screen5" src="https://github.com/user-attachments/assets/45e9a6c1-2457-401b-aa4e-eabc034363b9">

<img width="660" alt="Screen6" src="https://github.com/user-attachments/assets/a813ecb9-aeaf-4ead-bcbf-3db5efccfd6c">

<img width="574" alt="Screen7" src="https://github.com/user-attachments/assets/f9944ff0-a5c1-4f73-b6dc-4c65da5eaf6b">

4. Добавьте несколько assert в verify.yml-файл для  проверки работоспособности vector-role (проверка, что конфиг валидный, проверка успешности запуска и др.). 

<img width="352" alt="Screen8" src="https://github.com/user-attachments/assets/bb209d95-1c4e-4b6e-a44b-920dba0f5a6e">

[verify.yml](https://github.com/sash3939/Ansible5/blob/main/roles/test-role/molecule/default/verify.yml)

5. Запустите тестирование роли повторно и проверьте, что оно прошло успешно.
  
5. Добавьте новый тег на коммит с рабочим сценарием в соответствии с семантическим версионированием.

<img width="548" alt="Screen9" src="https://github.com/user-attachments/assets/dd018230-c249-427e-93ac-a2669a9c8976">

### Tox

1. Добавьте в директорию с vector-role файлы из [директории](./example).
2. Запустите `docker run --privileged=True -v <path_to_repo>:/opt/vector-role -w /opt/vector-role -it aragast/netology:latest /bin/bash`, где path_to_repo — путь до корня репозитория с vector-role на вашей файловой системе.
3. Внутри контейнера выполните команду `tox`, посмотрите на вывод.
5. Создайте облегчённый сценарий для `molecule` с драйвером `molecule_podman`. Проверьте его на исполнимость.
6. Пропишите правильную команду в `tox.ini`, чтобы запускался облегчённый сценарий.
8. Запустите команду `tox`. Убедитесь, что всё отработало успешно.
9. Добавьте новый тег на коммит с рабочим сценарием в соответствии с семантическим версионированием.

После выполнения у вас должно получится два сценария molecule и один tox.ini файл в репозитории. Не забудьте указать в ответе теги решений Tox и Molecule заданий. В качестве решения пришлите ссылку на  ваш репозиторий и скриншоты этапов выполнения задания. 

## Необязательная часть

1. Проделайте схожие манипуляции для создания роли LightHouse.
2. Создайте сценарий внутри любой из своих ролей, который умеет поднимать весь стек при помощи всех ролей.
3. Убедитесь в работоспособности своего стека. Создайте отдельный verify.yml, который будет проверять работоспособность интеграции всех инструментов между ними.
4. Выложите свои roles в репозитории.

В качестве решения пришлите ссылки и скриншоты этапов выполнения задания.

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.
