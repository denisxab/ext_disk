# Как развернуть свой Wireguard VPN сервер с WEB-интерфейсом за одну команду

WireGuard является одним из наиболее популярных и простых в использовании VPN-решений, предоставляющих безопасное сетевое соединение. Если вы ищете быстрый и простой способ развернуть собственный VPN-сервер WireGuard с WEB-интерфейсом, то Docker-контейнер представляет отличное решение. В этой статье мы рассмотрим, как установить и запустить Docker-контейнер WireGuard с WEB-интерфейсом за одну команду, а также как подключиться к нему с различных устройств.

## Сервер

### Развертывание WireGuard WEB UI сервера через Docker

#### Предварительные настройки

Для начала необходимо установить `Ansible`, инструмент автоматизации развертывания приложений на удаленных серверах. Выполните следующую команду для установки Ansible:

```bash
sudo apt install ansible
```

Также чтобы `ansible` подключатся к удаленному серверу через пароль установите:

```bash
sudo apt install sshpass
```

Далее создайте файл `inventory.yml`, в котором нужно указать данные для подключения к серверу, например:

```yml
---
all:
    hosts:
        ИмяСервера1:
            ansible_host: IP_Адрес
            ansible_user: Пользователь
            # SSH порт
            ansible_port: 22
            # Для этого устанавливали sshpass
            ansible_ssh_pass: Пароль
```

Замените `ИмяСервера`, `IP_Адрес`, `Пользователь` и `Пароль` на соответствующие значения для вашего сервера.

#### Вот та единственная команда

Теперь можно выполнить команду для развертывания WireGuard WEB UI сервера с помощью Docker-контейнера:

```bash
ansible-playbook -i ./inventory.yml -l ИмяСервера1 ./wireguard/install_wireguard_server.yml -e PasswordServer=990990
```

Здесь `ИмяСервера` - имя вашего сервера, `PasswordServer` - пароль для WEB-версии WireGuard. После успешного выполнения команды, WEB-версия WireGuard будет доступна по URL: `IP_Адрес:51821`. По умолчанию пароль `990990`

## Клиент

### Телефон

Чтобы подключиться к VPN-серверу WireGuard с вашего телефона, выполните следующие шаги:

1. Установите приложение WireGuard на свой телефон.
2. Отсканируйте QR-код, как показано на скриншоте ниже:

    - ![Скриншот 1](./img/Screenshot_20230528_000435.png)
    - ![Скриншот 2](./img/Screenshot_20230528_000528.png)

3. Нажмите "Добавить" и сохраните настройки VPN.

### Linux

Для подключения к VPN-серверу WireGuard на Linux выполните следующие шаги:

1. Получите файл конфигурации для подключения к VPN-серверу. Выглядит он примерно так:

    ![Сконфигурации](./img/Screenshot_20230527_235935.png)

2. Скопируйте файл конфигурации в папку `/etc/wireguard/` с помощью следующей команды:

    ```bash
    cp ИмяКонфигурации.conf /etc/wireguard/
    ```

3. Подключитесь к VPN-серверу WireGuard с помощью следующей команды:

    ```bash
    sudo wg-quick up ИмяКонфигурации
    ```

4. Чтобы отключиться от VPN, выполните следующую команду:

    ```bash
    sudo wg-quick down ИмяКонфигурации
    ```

Теперь у вас есть свой собственный WireGuard VPN сервер с WEB-интерфейсом, развернутый с помощью Docker-контейнера. Вы можете подключиться к нему с различных устройств, включая телефоны и компьютеры с Linux. WireGuard предоставляет безопасное и эффективное шифрованное соединение, которое защищает вашу приватность и обеспечивает безопасность передачи данных в интернете.

# Как развернуть NextCloud на HTTPS за одну команду

## Вот та единственная команда

Пример взят из https://github.com/nextcloud/docker/tree/master/.examples/docker-compose/insecure/postgres/fpm

1. Чтобы передать эти переменные из командной строки при запуске `docker-compose`, выполните следующую команду:

    ```bash
    ansible-playbook -i ./inventory.yml -l ИмяСервера1 ./nextcloud/install_nextcloud_server.yml -e POSTGRES_PASSWORD=10101010
    ```

    - `POSTGRES_PASSWORD` = Пароль от базы данных PostgreSQL

2. Подождать 2 минуты запуска всех приложений
3. Перейти на URL `https://Хост`
4. Создать учетную запись администратора.
   Например:
    - User: nextcloud
    - Password: nextcloud10101010
5. **Выбираем пропустить рекомендуемые расширения**

## Сделать Backup всех файлов NextCloud через RSYNC

```bash
ansible-playbook -i ./inventory.yml -l ИмяСервера1 ./nextcloud/backup_nextcloud_server.yml -e LOCAL_PATH_BACKUP="$HOME/backup_nextcloud"
```

-   `LOCAL_PATH_BACKUP` = Путь на локальной машине, куда сохранить бекап
