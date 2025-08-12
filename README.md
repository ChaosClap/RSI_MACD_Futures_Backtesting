# ZRSIMACD (modular) — RSI/MACD утилиты и сбор котировок

Репозиторий упакован в пакет со структурой `src/`. Все старые скрипты сохранены и доступны как подкоманды CLI.

## Установка (локально)
```bash
python -m venv .venv && source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -U pip
pip install -e .
cp .env.example .env  # заполните TINKOFF_TOKEN
mkdir -p data && cp src/zrsimacd/scripts/../..//data/tickers.txt.example data/tickers.txt 2>/dev/null || true
```

## Использование
```bash
# Загрузка свечей через Tinkoff
zrsimacd fetch

# Работа с фьючерсами
zrsimacd futures

# Расчёт индикаторов по CSV
zrsimacd indicators

# Финальный анализ RSI/MACD
zrsimacd analyze

# Отчёты по трейдам
zrsimacd report
```

Любые аргументы после подкоманды пробрасываются в оригинальный скрипт, например:
```bash
zrsimacd fetch --help
```

## Структура
- `src/zrsimacd/scripts/` — первичные скрипты (без переписывания логики).
- `src/zrsimacd/cli.py` — единая точка входа (CLI).
- `.env.example` — задаёт `TINKOFF_TOKEN`, `TICKERS_FILE` и пр.
- `pyproject.toml` — метаданные и зависимости.


## 📂 Путь для данных

- **Список тикеров** — файл `data/tickers.txt` (каждый тикер на новой строке, пример в `data/tickers.txt.example`).
- **Токен Tinkoff Invest API** — храните в `.env` (`TINKOFF_TOKEN=...`) или в `token.txt` (не рекомендуется).
- **Котировки** — после выполнения команды `zrsimacd fetch` будут сохранены в папке `SBERBANK_FUTURES/` в корне проекта.  
  Внутри будет структура по интервалам из `INTERVALS` (например: `SBERBANK_FUTURES/4_hour/SBER.csv`).

**Пример структуры:**
```
SBERBANK_FUTURES/
└── 4_hour/
    ├── SBER.csv
    ├── GAZP.csv
    └── ...
```

## Лицензия
MIT