# nginx-systemd-lab

Учебный проект: запуск nginx с кастомным конфигом под управлением systemd.

## Что делает
Поднимает nginx на порту 8080, отдаёт статическую страницу, пишет логи в локальную папку. Управляется через собственный unit-файл systemd с автоперезапуском при падении.

## Стек
Linux (systemd), nginx.

## Запуск
1. Скопировать unit-файл:
   ```bash
   sudo cp nginx-lab.service /etc/systemd/system/
   sudo systemctl daemon-reload