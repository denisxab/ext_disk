Это проект для создания собственного удаленного хранилища

В качестве платы будет использован Orange pi zero 2

Доступ к удаленному хранилищу будет производиться через Wireguard VPN

Источник: https://notabug.org/Black_Triangle/Manual_Nextcloud_on_Orange_Pi

# Настройка Wireguard VPN

## Сервер

### Развертывание Wireguard WEB UI сервера через Docker

Установить и запустить Docker контейнер в WireGuard с WEB интерфейсом

```bash
ansible-playbook -i ./WireguardVPN/inventory.yml -l reg_ru ./WireguardVPN/ansibel/install_docker_server.yml -e PasswordServer=990990
```

-   `PasswordServer` - Указать пароль для WEB версии WireGuard

После этого WEB версия доступна по URL: `Хост:51821`

## Клиент

### Телефон

1. ![](./img/Screenshot_20230528_000435.png)
2. ![](./img/Screenshot_20230528_000528.png)

### Linux

### Подключение к VPN

1. Получить файл конфигурации для подключения к VPN

    ![](./img/Screenshot_20230527_235935.png)

2. Скопировать этот файл конфигурации в папку

    ```bash
    cp ИмяКонфигурации.conf /etc/wireguard/
    ```

3. Подключение к VPN

    ```bash
    sudo wg-quick up ИмяКонфигурации
    ```

4. _Отключение от VPN_

    ```bash
    sudo wg-quick down ИмяКонфигурации
    ```
