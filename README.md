# YarkiLab – автопостинг

Здесь только запуск. Код живёт в закрытом движке YarkiLab и обновляется сам. Настройки и ключи хранятся в **секретах** репозитория, их не видит никто, кроме владельца.

## Установка (5 минут)

1. Нажмите **Use this template → Create a new repository**, выберите **Private**.
2. **Settings → Secrets and variables → Actions → New repository secret** – добавьте секреты из списка ниже (только нужные площадки).
3. **Actions → YarkiLab – автопостинг → Run workflow** – первый запуск. Дальше всё работает само каждые 30 минут.

## Секреты

| Секрет | Что это |
|---|---|
| `ENGINE_TOKEN` | ключ доступа к движку (выдаёт специалист) |
| `PROJECTS` | настройки проектов (готовый текст выдаёт мастер установки) |
| `GOOGLE_CREDENTIALS` | ключ Google-робота, который читает таблицы (выдаёт специалист) |
| `SPREADSHEET_ID` | ID таблицы автопубликаций |
| `TG_BOT_TOKEN`, `TG_CHANNEL_ID` | бот-публикатор Telegram и канал |
| `TG_MATERIALS_BOT_TOKEN` | бот канала-базы материалов |
| `TG_MIRROR_BOT_TOKEN` | бот-зеркало TG → Max (если нужно) |
| `MAX_TOKEN`, `MAX_CHANNEL_ID` | бот и канал Max |
| `VK_TOKEN`, `VK_OWNER_ID` | ключ сообщества VK и ID сообщества со знаком минус |
| `THREADS_APP_ID`, `THREADS_APP_SECRET`, `IG_APP_ID`, `IG_APP_SECRET` | приложения Meta для Threads и Instagram |

Несколько проектов: у второго и следующих задайте `prefix` (например `"P2_"`) и добавляйте их ключи с этой приставкой: `P2_TG_BOT_TOKEN` и т. д.
