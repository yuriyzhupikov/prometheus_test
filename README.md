# Prometheus
___
### Для работы Prometheus понадобится:
``Prometheus``
``Node_exporter``
``Alertmanager``
``Client_golang``
``Pushgateway``
___
### Prometheus - сервер запрашиваюший метрики различных сервисов 
#### Установка
1. ``git clone repo``
2. [Находим билд](https://github.com/prometheus/prometheus/releases "https://github.com/prometheus/prometheus/releases") под свою платформу (например linux-amd64)
3. Скачиваем билд``wget <path_to_build>``
4. Разархивируем ``tar -xf prometheus-*.tar.gz``
5. Исполняемы файлы перемещаем в ``/usr/local/bin``:
- Переходим в папку ``cd prometheus-*``
- Копируем два файла``cp prometheus promtool /usr/local/bin``
6. Создаём две папки``/etc/prometheus /var/lib/prometheus``:
- ``mkdir /etc/prometheus`` - для хранения конфига prometheus
- ``mkdir /var/lib/prometheus`` - для хранения данных (метрики)
7. Копируем файл конфига в``/etc/prometheus``:
- ``cp prometheus.yml /etc/prometheus``
8. Дополнительно можно создать пользователя и группу:
- ``useradd --no-create-home --home-dir / --shell /bin/false prometheus``
- ``chown -R prometheus:prometheus /var/lib/prometheus``
9. Создаём символью ссылку на ``promethus.service``:
- ``sudo ln ./prometheus.service /etc/systemd/system/prometheus.service``
10. Запускаем Prometheus server:
- ``systemctl daemon-reload``
- ``systemctl start prometheus``
11. Перейти по адресу http://localhost:9090 (по умолчанию)
___
###Node_exporter
Позволяет измерять различные ресурсы машины, такие как использование памяти, диска и процессора
#### Установка

``Скачиваем`` [билд](https://github.com/prometheus/node_exporter/releases "https://github.com/prometheus/node_exporter/releases")

```$ wget https://github.com/.../node_exporter-0.18.1.linux-amd64.tar.gz
$ tar xf node_exporter-*.tar.gz
$ cd node_exporter-*
$ cp node_exporter /usr/local/bin
$ useradd --no-create-home --home-dir / --shell /bin/false node_exporter
```
Создаём символьную ссылку

```sudo ln ./node_exporter.service /etc/systemd/system/node_exporter.service```

Запускаем
```$ systemctl daemon-reload
$ systemctl start node_exporter
$ systemctl status node_exporter
```
Тест

``curl -s http://localhost:9100/metrics`` (Увидим множество данных о железе)

___

###Alertmanager
...