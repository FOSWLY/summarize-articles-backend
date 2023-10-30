## [FOSWLY] Summarize Backend

[![Python Version](https://img.shields.io/badge/Python-3.11-blue?logo=python&style=for-the-badge)](https://www.python.org/)
[![GitHub Stars](https://img.shields.io/github/stars/FOSWLY/summarize-backend?logo=github&style=for-the-badge)](https://github.com/FOSWLY/summarize-backend/stargazers)
[![GitHub Issues](https://img.shields.io/github/issues/FOSWLY/summarize-backend?style=for-the-badge)](https://github.com/FOSWLY/summarize-backend/issues)
[![Current Version](https://img.shields.io/github/v/release/FOSWLY/summarize-backend?style=for-the-badge)](https://github.com/FOSWLY/summarize-backend)
[![GitHub License](https://img.shields.io/github/license/FOSWLY/summarize-backend?style=for-the-badge)](https://github.com/FOSWLY/summarize-backend/blob/master/LICENSE)

**[FOSWLY] Summarize Backend** - cервер, который реализует Yandex Summarize API для нашего браузерного расширения. Сервер не содержит никакой авторизации и может быть использован для ваших проектов.

## 📝 Функционал
- Суммаризатор статей
- Суммаризатор видео

## 📦 Деплой
1. Установите Python 3.11 (на других версиях не тестировался)
2. Клонируйте репозиторий
3. Установите зависимости: `pip install -r requirements.txt`
4. Заполните конфиг: `app/settings.py`
5. Переименуйте `.example.env` --> `.env`
6. Заполните: `.env`
7. Запустите сервер: `python3 -OO main.py`

## ⚙️ Заполнение .env
1. Переименуйте `.example.env` в `.env`
2. Получение `API_KEY`:
   1. Перейдите на сайт [300.ya.ru](https://300.ya.ru/)
   2. Внизу нажмите на "API"
   3. В появившейся панельке нажмите "Получить токен"
   4. Авторизуйтесь, если вы не авторизованы
   5. Вставьте полученный токен в `.env`
3. Получение `YANDEX_COOKIE`:
   1. Перейдите на сайт [300.ya.ru](https://300.ya.ru/)
   2. Авторизуйтесь, если вы не авторизованы. Лучше всего использовать не основной аккаунт, поскольку **все действия выполняются на ваш страх и риск**.
   3. Откройте DevTools (F12 или Ctrl+Shift+I)
   4. Перейдите в Application

        P.S. В некоторых браузерах этого пункта нету. В них вы должны сразу перейти в Storage.
   5. Выберите Storage
   6. Выберите Cookies
   7. Найдите куки с именем `Session_id` и скопируйте ее значение
   8. Вставьте скопированное значение заместо XXXX в `.env`

## 📖 Зачем нужен свой сервер, почему бы не использовать API напрямую?
В использование API напрямую есть несколько проблемы из-за которых мы от этого отказались:
1. Для работы с Yandex Summarize API нужна авторизация, т.е. необходимо посылать запросы с токеном/куки, которые не хотелось бы лишний раз "палить" на клиенте.
2. Браузерные расширения сначало посылают OPTIONS запрос, а уже потом обычный запрос. Отсюда вытекает то, что YandexAPI блокирует OPTIONS запрос как "не авторизованный" и расширение не может получить данные с сервера. Возможно, это можно было решить более легким путем, но я не разобрался как.
3. У некоторых пользователей могут быть заблокированы сервера Yandex и прямой запрос бы просто не прошёл.