Деплой

```bash
ansible-playbook -i inventory.yml -l netherlands_wireguard neko_deploy.yml -e NEKO_PASSWORD_ADMIN="denis0303"
```

Войти

```bash
http://IP:8080/
admin
denis0303
```

# Установка Microsoft Edge

```bash
sudo apt update
sudo apt install software-properties-common apt-transport-https wget
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/edge stable main"
sudo apt install microsoft-edge-dev
sudo apt update
sudo apt upgrade
```

Использование

```bash
sudo -su root
```

```bash
microsoft-edge --no-sandbox
```
