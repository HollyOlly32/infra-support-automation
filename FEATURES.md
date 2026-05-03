# 🎯 Что вы получите после запуска playbook 

## Кратко
Полностью настроенная рабочая станция Support Engineer для High-load среды с Docker, PostgreSQL, мониторингом и всеми необходимыми утилитами.

---

## 📦 Что будет установлено

### 1. Системные утилиты для диагностики
- `htop` — мониторинг процессов в реальном времени
- `curl/wget` — HTTP-клиенты для API запросов
- `git` — система контроля версий
- `net-tools` — ifconfig, netstat, route (диагностика сети)
- `vim` — редактирование конфигов
- `netcat-openbsd` — отладка сети
- `openvpn` — VPN клиент
- `ca-certificates`, `apt-transport-https` — безопасные репозитории

### 2. Docker + PostgreSQL 15 (тестовая БД)
- Контейнер: `test_trading_db`
- Порт: `5432` (доступен локально)
- Пользователь: `postgres`
- База данных: `trading_db`
- Данные сохраняются в: `/opt/postgres_data/`
- Healthcheck — автоматическая проверка работоспособности

### 3. Prometheus Node Exporter (мониторинг)
- Порт: `9100`
- Метрики: CPU, Memory, Disk, Network, Load Average, Uptime
- Сервис: автоматически запускается при загрузке системы
- Работает от изолированного пользователя `node_exporter`

### 4. OpenVPN (готов к подключению)
- Конфиг: `/etc/openvpn/client/office_vpn.conf`
- Сервис: `openvpn-client@office_vpn`
- Осталось только добавить сертификаты и запустить

### 5. Bash алиасы (ускорение работы)

| Алиас | Команда | Что делает |
|-------|---------|-------------|
| `check_app_logs` | `grep -i "error" /var/log/syslog \| tail -20` | Показывает последние 20 ошибок |
| `watch_logs` | `tail -f /var/log/syslog` | Мониторит логи в реальном времени |
| `check_ports` | `netstat -tulpn \| grep LISTEN` | Показывает все слушающие порты |
| `docker_stats` | `docker stats --no-stream` | Статистика Docker контейнеров |
| `psql_trading` | `docker exec -it test_trading_db psql -U postgres` | Подключается к тестовой БД |
| `dps` | `docker ps --format "table {{.Names}}\t{{.Status}}\t{{.Ports}}"` | Красивый список контейнеров |
| `dlogs` | `docker logs -f` | Логи контейнера в реальном времени |

---

## 🚀 Что вы сможете делать сразу после установки

### Диагностика инцидентов
```bash
check_app_logs          # найти ошибки в логах
check_ports             # проверить какие сервисы слушают порты
watch_logs              # мониторить логи в реальном времени
