## ДЗ (ELK) - Beats - инструменты доставки данных.

---
## Требования:

* [Docker Engine][docker-install] version **18.06.0** or newer
* [Docker Compose][compose-install] version **2.0.0** or newer
* 1.5 GB of RAM

# Установка и запуск проекта:

Склонировать репозиторий:

```sh
git clone https://github.com/headsinjars/ELK.git
```

Выполнить инициализацию пользователей и групп Elasticsearch

```sh
docker compose up setup
```

Сгенерировать ключи шифрования для  Kibana используя следующую команду и скопировать вывод команды
в конфигурационный файо Kibana (`kibana/config/kibana.yml`):

```sh
docker compose up kibana-genkeys
```

Запустить компоненты стэка:

```sh
docker compose up -d
```

---

Подождите несколько минут для полного запуска.
Первычные данные для входа

* user: *elastic*
* password: *changeme*

---

## Сделано:

1. Развернут filebeat с модулями nginx и mysql для сбора логов (файл конфигурации: filebeat/filebeat.yml)
В настройках каждый лог узла попадает в свой отдельный индекc.
2. Развернут metricbeat для сбора метрик (файл конфигурации: metricbeat/metricbeat.yml)
3. Развернут heartbeat для статуса доступности CMS и MySQL
4. Настроены политики хранения логов (настроены ILM с более высоким приоритетом). Все новые шаблоны индексов попадают под действие
ILM с более высоким приоритетом.
5. В filebeat приведен конфиг для dissect nginx, но он закоментирован и приведен исключительно в качестве наглядности, т.к. "разбор" лога на типовые
поля выполняется модулем nginx.
6. Скриншоты дэшбордов приведены в каталоге screenshots.
