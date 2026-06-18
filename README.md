<div align="center">

<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&height=280&color=0:0F0717,30:1A102B,70:7C3AED,100:A855F7&text=KREST&fontColor=FFFFFF&fontSize=90&fontAlignY=40&animation=fadeIn[...]>

# ⚡ KREST

### Терминальный AI‑ассистент для разработки и автоматизации

> **Code. Search. Execute. All from your terminal.**

<br>

![Python](https://img.shields.io/badge/Python-3.9+-7C3AED?style=for-the-badge&logo=python&logoColor=white)
![OpenRouter](https://img.shields.io/badge/OpenRouter-A855F7?style=for-the-badge)
![Rich](https://img.shields.io/badge/Rich_UI-C084FC?style=for-the-badge)
![CLI](https://img.shields.io/badge/CLI-Terminal-9333EA?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-581C87?style=for-the-badge)

</div>

---

## ⚡ О KREST

KREST — терминальный AI‑ассистент, объединяющий LLM‑модели (через OpenRouter) с реальными инструментами: чтение/запись файлов, запуск команд, поиск и скачивание страниц, обработка мультимедиа и опционально — интеграция с Telegram. Всё из терминала, с сессиями и памятью.

Основные сценарии использования: генерация/правка кода, исследование (research), автоматизация задач, быстрый доступ к внешним источникам (веб/YouTube), и взаимодействие через Telegram‑бот (опционально).

---

## 🟣 Что нового (из KREST.py)

- Автоустановка отсутствующих зависимостей при первом запуске (pip install ...), чтобы минимизировать ручную настройку.
- Поддержка дополнительных опциональных пакетов:
  - youtube_transcript_api, yt‑dlp — получение и скачивание аудио/транскриптов с YouTube
  - trafilatura — извлечение содержимого веб‑страниц в Markdown
  - duckduckgo_search / ddgs — быстрый поиск
  - pyTelegramBotAPI (telebot) — Telegram‑бот
- Расширенный веб‑фетчинг:
  - автоматическое извлечение текста страниц (trafilatura), список ссылок на странице;
  - YouTube: попытка получить субтитры через youtube_transcript_api; при отсутствии — метаданные; при наличии OPENROUTER_TOKEN — загрузка аудио через yt‑dlp и транскрипция Whisper (OpenRouter).
  - fallback‑скраппинг Google/Bing при отсутствии DDG‑модуля.
- Теги/операции в тексте:
  - [SEARCH:query], [FETCH:url], [READ:path], [WRITE:path::content], [RUN:command] — KREST выполняет и вставляет результаты.
  - Добавлены теги/механики для памяти и навыков: [LEARN:], [SKILL:...].
- Telegram‑бот (опционально):
  - команда /tgbot для запуска/настройки;
  - поддержка навыков (skills): добавление, импорт из файла, переключение, триггеры;
  - бот извлекает кодовые блоки и отправляет их как файлы.
  - конфигурация сохраняется в ~/KREST/tgbot_config.json.
- Система памяти и сессий:
  - автосохранение сессий в ~/KREST/memory/*.json;
  - команды для просмотра/загрузки/экспорта сессий (/memory, /sessions, /load, /save, /export).
  - хранилище ограничено (очистка старых сессий).
- Управление моделями через OpenRouter:
  - по умолчанию MODEL = "nousresearch/hermes-4-405b";
  - API_URL = "https://openrouter.ai/api/v1/chat/completions";
  - команды /models (список), /model <name> (выбор).
- Автоматическое обнаружение и предобработка URL в сообщениях; если передан URL — KREST подгрузит содержимое и подставит его в контекст запроса.

---

## 🟢 Возможности

- Генерация кода и правки прямо в терминале
- Поиск по вебу и интеграция результатов в ответы
- Чтение и запись файлов в проекте
- Выполнение shell‑команд и показ вывода
- Сохранение и восстановление сессий
- Опциональный Telegram‑бот с навыками (skills)
- Поддержка YouTube‑транскриптов и аудио‑транскрипции через OpenRouter (Whisper)
- Автоустановка недостающих зависимостей при запуске

---

## 🚀 Установка

Клонируйте репозиторий:

```bash
git clone https://github.com/Pre11yhacker/KREST.git
cd KREST
```

Установите основные зависимости:

```bash
pip install rich python-dotenv ddgs psutil
```

Опционально рекомендуется установить дополнительные пакеты для расширенного функционала:

```bash
pip install duckduckgo-search youtube-transcript-api yt-dlp trafilatura pyTelegramBotAPI
```

Заметки:
- KREST при запуске попытается автоматически установить отсутствующие пакеты (через pip).
- Для работы с YouTube‑аудио и транскрипцией может потребоваться ffmpeg в системе.

Запуск:

```bash
python KREST.py
```

---

## 🔑 OpenRouter API Key

При первом запуске KREST запросит OPENROUTER_TOKEN и попробует сохранить его в ~/.KREST/.env (WORKSPACE = ~/KREST). Можно получить ключ на:

https://openrouter.ai/keys

Команда /token позволяет просмотреть или обновить ключ во время сессии; /deletekey — удалить ключ с диска и из памяти.

---

## 📂 Структура рабочего каталога (WORKSPACE)

По умолчанию WORKSPACE = ~/KREST

```text
~/KREST
│
├── .env                   # OPENROUTER_TOKEN при сохранении
├── tgbot_config.json      # (опционально) конфигурация Telegram бота
│
├── memory/                # сохранённые сессии JSON
│   ├── session_2023...json
│   └── ...
│
├── skills/                # (Telegram) сохранённые навыки (json)
│   ├── myskill.json
│   └── ...
│
├── code/                  # (пользовательская зона)
├── logs/
└── exports/
```

---

## 🛠 Команды (терминал)

| Команда      | Описание                                  |
| ------------ | ----------------------------------------- |
| /help        | Показать справку                          |
| /clear       | Очистить историю                          |
| /reload      | Перезагрузить системный prompt            |
| /context     | Статистика контекста                      |
| /sys         | Информация о системе                      |
| /stats       | Использование ресурсов (CPU/RAM/Disk)     |
| /model       | Текущая модель или /model <name>          |
| /models      | Показать все модели на ключе OpenRouter   |
| /token       | Показать/обновить OPENROUTER_TOKEN       |
| /deletekey   | Удалить ключ из .env и памяти             |
| /memory      | Последние сессии (10)                     |
| /sessions    | Все сессии (30)                           |
| /save        | Сохранить текущую сессию                  |
| /load <id>   | Загрузить сессию                          |
| /export      | Экспортировать сессию                     |
| /input <file>| Отправить файл как сообщение              |
| /tgbot       | Запустить/остановить Telegram‑бот         |
| /exit        | Выйти из KREST                            |

Доп. теги (в тексте/сообщении):
- [SEARCH:query] — выполнить веб‑поиск и вернуть результаты
- [FETCH:url] — скачать и извлечь содержимое страницы
- [READ:path] — прочитать локальный файл
- [WRITE:path::content] — записать файл
- [RUN:command] — выполнить команду в shell

---

## 🔍 Специальные операции

Примеры:

Search:
```text
[SEARCH:python asyncio tutorial]
```

Read:
```text
[READ:main.py]
```

Write:
```text
[WRITE:app.py::print("hello")]
```

Run:
```text
[RUN:python app.py]
```

YouTube / multimedia:
- KREST сначала пытается получить субтитры через youtube_transcript_api;
- если есть OPENROUTER_TOKEN, KREST может скачать аудио (yt‑dlp) и отправить на транскрипцию Whisper (через OpenRouter API).

---

## 🧠 Система памяти и навыков (Skills)

- KREST автоматически сохраняет сессии в ~/KREST/memory.
- Через Telegram‑бот возможна работа с «навыками» (skills): создание, импорт (JSON или .skill), переключение on/off, триггеры.
- Теги [LEARN:...] позволяют боту добавлять факты в локальную память пользователя.

---

## 🌙 Тема и интерфейс

KREST использует тёмную палитру и библиотеку Rich для современного терминального интерфейса (если установлена). При отсутствии Rich интерфейс остаётся ANSI‑совместимым.

---

## 🧩 Поддерживаемые модели

KREST работает с моделями, доступными через OpenRouter. По умолчанию:
- MODEL = nousresearch/hermes-4-405b
- API_URL = https://openrouter.ai/api/v1/chat/completions

Переключайте модель командами /models и /model.

---

## 🔥 Собрано с использованием

- Python
- OpenRouter API
- Rich
- ddgs / duckduckgo_search
- python-dotenv
- psutil
- (опционально) yt-dlp, youtube-transcript-api, trafilatura, pyTelegramBotAPI

---

## 📜 Лицензия

MIT License

---

<div align="center">

## ⚡ KREST

### Терминальный AI — быстрое прототипирование и автоматизация

<p>
Built for developers • automation • cybersecurity • research
</p>

<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&section=footer&height=180&color=0:0F0717,30:1A102B,70:7C3AED,100:A855F7"/>

</div>
