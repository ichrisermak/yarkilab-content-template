# Контент-студия — мои проекты

Это клиентский репозиторий: в нём только запуск. Код автопостинга живёт в общем движке `ichrisermak/content-engine` и обновляется сам.

Репозиторий открытый, потому что у открытых репозиториев время работы GitHub Actions бесплатное. Все настройки и ключи хранятся в **секретах** (Settings → Secrets and variables → Actions). Их не видит никто, кроме владельца.

## Секреты

| Секрет | Что это |
|---|---|
| `PROJECTS` | список проектов (JSON, пример ниже) |
| `GOOGLE_CREDENTIALS` | JSON ключа сервисного аккаунта Google (общий для всех проектов) |
| `SPREADSHEET_ID` | ID таблицы автопубликаций |
| `TG_BOT_TOKEN`, `TG_CHANNEL_ID` | бот-публикатор Telegram и канал (@username или -100…) |
| `TG_MIRROR_BOT_TOKEN` | бот-зеркало TG → Max (если нужно) |
| `TG_MATERIALS_BOT_TOKEN` | бот канала-базы материалов (для расшифровки) |
| `MAX_TOKEN`, `MAX_CHANNEL_ID` | бот и канал Max |
| `VK_TOKEN`, `VK_OWNER_ID` | ключ сообщества VK и ID сообщества со знаком минус |
| `THREADS_APP_ID`, `THREADS_APP_SECRET`, `IG_APP_ID`, `IG_APP_SECRET` | приложения Meta для Threads и Instagram |

**Несколько проектов.** У второго и следующих проектов задайте `prefix`, например `"P2_"`, и добавляйте их ключи с этой приставкой: `P2_TG_BOT_TOKEN`, `P2_SPREADSHEET_ID` и т. д. Секреты без приставки (например, `GOOGLE_CREDENTIALS`) общие для всех проектов.

## Пример `PROJECTS`

```json
[
  {
    "id": "homeo",
    "name": "Гомеопатия просто",
    "prefix": "",
    "env": {
      "FOOTER_LINKS": "VK=https://vk.ru/…\nTG=https://t.me/…\nДЗЕН=https://dzen.ru/…\nMAX=https://max.ru/…",
      "ACCOUNTS": { "anna": "@doc.startseva.anna", "prosto": "@homeopathy_prosto" },
      "IG_DEFAULT": "prosto",
      "REDIRECT_URI": "https://ваш-сайт.ru/",
      "MATERIALS_SPREADSHEET_ID": "ID таблицы материалов",
      "MATERIALS_SHEET": "Наличие материалов",
      "DRIVE_FOLDER_ID": "ID папки «Подкасты на расшифровку»",
      "WHISPER_PROMPT": "Термины проекта для точной расшифровки"
    }
  }
]
```

## Запуск по расписанию

GitHub сам запускает автопостинг не чаще раза в 15 минут, и то нестабильно. Поэтому каждые 5 минут его запускает cron-job.org:

- адрес: `https://api.github.com/repos/<владелец>/<репозиторий>/actions/workflows/publish.yml/dispatches`
- метод POST, тело `{"ref":"main"}`
- заголовки: `Accept: application/vnd.github+json`, `X-GitHub-Api-Version: 2022-11-28`, `Content-Type: application/json`, `Authorization: Bearer <токен GitHub с правом Actions: Read and write>`
