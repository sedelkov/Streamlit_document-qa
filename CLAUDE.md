# CLAUDE.md — streamlit_document-qa

Инструкция для Claude Code. Общение с владельцем — по-русски.

> **Репозиторий ПУБЛИЧНЫЙ** (лицензия Apache-2.0). Всё, что попадает в git, видно всем. Ничего личного: ни персональных данных, ни рабочих материалов, ни ключей.

## Что это

Нетронутый шаблон Streamlit Community Cloud «Document question answering»: пользователь вводит свой ключ OpenAI в интерфейсе, загружает `.txt` или `.md`, задаёт вопрос — `gpt-3.5-turbo` отвечает потоком. Один файл `streamlit_app.py`, зависимости `streamlit` и `openai`. Состояние — шаблон, 1 коммит (январь 2025), своих изменений нет.

## С чего начать

1. `streamlit_app.py` (около 60 строк) и `README.md`.
2. `python3 -m venv .venv && . .venv/bin/activate && pip install -r requirements.txt` (версии не закреплены).
3. Тестов нет. Проверка: `python -m py_compile streamlit_app.py`, затем запуск и ручная проверка в браузере.

## Карта кода

| Путь | Что там |
|---|---|
| `streamlit_app.py` | всё приложение: поле ключа, загрузка файла, запрос к OpenAI |
| `requirements.txt` | `streamlit`, `openai` |
| `.devcontainer/devcontainer.json` | Codespaces: Python 3.11, автозапуск на порту 8501 |
| `.github/CODEOWNERS` | остался от шаблона (`@streamlit/community-cloud`) |

## Переменные окружения

Нет. Ключ OpenAI вводится в интерфейсе и живёт только в сессии. Альтернатива — `.streamlit/secrets.toml` (в `.gitignore`); никогда не коммитить и не просить ключ в чат. Вызовы OpenAI платные — только после «да» владельца.

## Запуск и деплой

- Локально: `streamlit run streamlit_app.py` → http://localhost:8501.
- Деплой: Streamlit Community Cloud из этого репозитория. Если на своём сервере — отдельная папка `/opt/streamlit_document-qa`, свой `docker compose`, сначала `free -h`, `df -h`, `docker ps`, ничего чужого не трогать, только после «да» владельца.

## Правила

- Изменения только через ветку и pull request на приёмку владельцу.
- Сначала требование и критерий приёмки, потом тест (pytest, без сети — клиент OpenAI подменять), потом код.
- `gpt-3.5-turbo` устарел: при доработке модель выбирать вместе с владельцем.
