# nginx-systemd-lab

[English](#english) | [Русский](#русский)

---

## Русский

Учебный проект: запуск nginx с кастомным конфигом под управлением systemd, с reverse proxy и автоперезапуском.

**Стек:** Linux (systemd), Nginx, Python (для тестового бэкенда).

**Запуск:**
1. Скопировать unit-файл:
   ```bash
   sudo cp nginx-lab.service /etc/systemd/system/
   sudo systemctl daemon-reload
   ```
2. Запустить: `sudo systemctl start nginx-lab`
3. Проверить: `curl http://localhost:8080` и `curl http://localhost:8080/app/`
**Важно перед запуском:** Скопируйте проект в `/opt/nginx-systemd-lab` (или измените пути в `nginx.conf` и `nginx-lab.service` на актуальные). Также замените `User=qbd` в `nginx-lab.service` на вашего пользователя.

**Что ломалось и как починил:**
1. Nginx не мог писать в `/var/log/nginx/` из-за прав. Вынес логи в локальную папку `logs/`.
2. Systemd не подхватывал новый unit. Забыл выполнить `daemon-reload`.
3. Nginx «падал» сразу после старта. Добавил `Type=forking` и `PIDFile`, так как nginx форкается.

**Ограничения:** Нет HTTPS (только HTTP). Статический конфиг.

**Лицензия:** MIT

---

## English

Educational project: running nginx with a custom config managed by systemd, including reverse proxy and auto-restart.

**Stack:** Linux (systemd), Nginx, Python (for test backend).

**Usage:**
1. Copy the unit file:
   ```bash
   sudo cp nginx-lab.service /etc/systemd/system/
   sudo systemctl daemon-reload
   ```
2. Start: `sudo systemctl start nginx-lab`
3. Check: `curl http://localhost:8080` and `curl http://localhost:8080/app/`
**Important before running:** Copy the project to `/opt/nginx-systemd-lab` (or update the paths in `nginx.conf` and `nginx-lab.service`). Also, change `User=qbd` in `nginx-lab.service` to your username.

**What broke & how I fixed it:**
1. Nginx couldn't write to `/var/log/nginx/` due to permissions. Moved logs to a local `logs/` folder.
2. Systemd didn't pick up the new unit. Forgot `daemon-reload`.
3. Nginx "crashed" right after start. Added `Type=forking` and `PIDFile` because nginx forks.

**Limitations:** No HTTPS (HTTP only). Static config.

**License:** MIT
