<h2 style="text-align: center;">[FOSWLY] Summarize Articles Backend</h2>

[![Python Version](https://img.shields.io/badge/Python-3.11-blue?logo=python&style=for-the-badge)](https://www.python.org/)
[![GitHub Stars](https://img.shields.io/github/stars/FOSWLY/summarize-articles-backend?logo=github&style=for-the-badge)](https://github.com/FOSWLY/summarize-articles-backend/stargazers)
[![GitHub Issues](https://img.shields.io/github/issues/FOSWLY/summarize-articles-backend?style=for-the-badge)](https://github.com/FOSWLY/summarize-articles-backend/issues)
[![Current Version](https://img.shields.io/github/v/release/FOSWLY/summarize-articles-backend?style=for-the-badge)](https://github.com/FOSWLY/summarize-articles-backend)
[![GitHub License](https://img.shields.io/github/license/FOSWLY/summarize-articles-backend?style=for-the-badge)](https://github.com/FOSWLY/summarize-articles-backend/blob/master/LICENSE)

**[FOSWLY] Summarize Articles Backend** - cервер, который реализует Yandex Summarize API для нашего браузерного расширения. Сервер не содержит никакой авторизации и может быть использован для ваших проектов.

## 📦 Деплой
1. Установите Python 3.11 (на других версиях не тестировался)
2. Клонируйте репозиторий
3. Установите зависимости: `pip install -r requirements.txt`
4. Заполните конфиг: `config/config.cfg`
5. Переименуйте `config/.example.env` --> `config/.env`
6. Заполните: `config/.env`
7. Запустите сервер: `python3 -OO main.py`


## 📖 Зачем нужен свой сервер, почему бы не использовать API напрямую?
В использование API напрямую есть несколько проблемы из-за которых мы от этого отказались:
1. Для работы с Yandex Summarize API нужна авторизация, т.е. необходимо посылать запросы с токеном/куки, которые не хотелось бы лишний раз "палить" на клиенте.
2. Браузерные расширения сначало посылают OPTIONS запрос, а уже потом обычный запрос. Отсюда вытекает то, что YandexAPI блокирует OPTIONS запрос как "не авторизованный" и расширение не может получить данные с сервера. Возможно, это можно было решить более легким путем, но я не разобрался как.
3. У некоторых пользователей могут быть заблокированы сервера Yandex и прямой запрос бы просто не прошёл.