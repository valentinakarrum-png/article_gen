# BigData Sports API — Быстрый старт

## Подключение

| Параметр | Значение |
|---|---|
| Base URL | `https://api.bigdatasports.io/v1` |
| Метод | только **GET** |
| Формат ответа | `application/json`, UTF-8 |
| Аутентификация | Заголовок `x-bds-api-key` |
| API-ключ | `c3499618cf23e0185d2ae9c9404b3021` |
| Время | ISO 8601, UTC+03:00 по умолчанию |

> **Важно:** Наша лицензия — только **футбол** (`sport_id=1`).
> Во всех запросах указывай `sport_id=1`. Другие виды спорта запрашивать **нельзя**.

---

## Пример запроса (curl)

```bash
curl -H "x-bds-api-key: c3499618cf23e0185d2ae9c9404b3021" \
  "https://api.bigdatasports.io/v1/matches?sport_id=1&date_from=2026-03-17&date_to=2026-03-17"
```

## Пример запроса (Python)

```python
import requests

API_KEY = "c3499618cf23e0185d2ae9c9404b3021"
BASE    = "https://api.bigdatasports.io/v1"
HEADERS = {"x-bds-api-key": API_KEY}

r = requests.get(f"{BASE}/matches", headers=HEADERS, params={
    "sport_id": 1,
    "date_from": "2026-03-17",
    "date_to":   "2026-03-17",
})
print(r.json())
```

---

## Все эндпоинты

### Справочники
| Эндпоинт | Описание |
|---|---|
| `/sports/list` | Виды спорта |
| `/countries/list` | Страны |
| `/bookmakers/list` | Букмекеры |
| `/competitions/list` | Турниры |
| `/teams/list` | Команды |
| `/players/list` | Игроки |
| `/coaches/list` | Тренеры |
| `/referees/list` | Судьи |

### Турниры
| Эндпоинт | Описание |
|---|---|
| `/competitions` | Инфо о турнире |
| `/competitions/by-country` | Турниры по странам |
| `/competitions/season` | Инфо по сезону |
| `/competitions/season_top_players` | Лучшие игроки сезона |
| `/competitions/standings-and-brackets` | Таблицы и сетки |

### Матчи
| Эндпоинт | Описание |
|---|---|
| `/matches` | Расписание и результаты (матч-центр) |
| `/matches/count` | Кол-во матчей по статусам |
| `/matches/odds` | Коэффициенты |
| `/matches/stats` | Статистика матча |
| `/matches/stats-list` | Статистика нескольких матчей |
| `/matches/timeline` | Таймлайн (голы, карточки...) |
| `/matches/lineup` | Составы |
| `/matches/predicted-lineup` | Предварительные составы |
| `/matches/sideliners` | Травмированные / дисквалифицированные |
| `/matches/prematch-summary` | Прематч-саммари |
| `/matches/point-by-point` | Очко за очком (теннис — не наш случай) |
| `/matches/updates` | Недавно обновлённые матчи |
| `/matches/match-ids-mappings` | Маппинг ID из других источников |

### Команды
| Эндпоинт | Описание |
|---|---|
| `/teams` | Инфо о команде |
| `/teams/avgs` | Средние показатели |
| `/teams/trends-streaks` | Тренды и серии |
| `/teams/h2h-trends` | Очные встречи (H2H) |
| `/teams/top` | Лучшие команды по тренду |
| `/teams/players` | Игроки команды |
| `/teams/profitability` | Прибыльность ставок |

### Игроки
| Эндпоинт | Описание |
|---|---|
| `/players` | Инфо об игроке |
| `/players/transfers` | Трансферы |

### Букмекеры
| Эндпоинт | Описание |
|---|---|
| `/bookmakers` | Инфо о букмекере |
| `/bookmakers/best-odds` | Лучшие коэффициенты |

### Судьи
| Эндпоинт | Описание |
|---|---|
| `/referees/avgs` | Средние показатели судьи |
| `/referees/trends` | Тренды судей |

### Прогнозы
| Эндпоинт | Описание |
|---|---|
| `/predictions` | Прематч-прогнозы |
| `/predictions/live` | Лайв-прогнозы |

---

## Формат ответа

Все ответы имеют одинаковую обёртку:

```json
{
  "success": true,
  "data": { ... },
  "error": null
}
```

При ошибке:
```json
{
  "success": false,
  "data": [],
  "error": "описание ошибки"
}
```

---

## Напоминания

1. **Только `sport_id=1`** — другие виды спорта не трогаем
2. API-ключ — **не коммитить** в публичные репозитории
3. Все методы — **GET**, тело запроса не нужно
4. Пагинация: `limit` + `page` (где поддерживается)
5. Исторические данные доступны **с 2015 года**
