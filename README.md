# PSUP-INFRASTRUCTURE_SERVICE

**PSUP-INFRASTRUCTURE_SERVICE** — сервис для запуска инфраструктуры универсальной платформы по дистрибуции товаров.

---

## Инфраструктура

- **Kafka** (в режиме KRaft)
- **Kafka UI**
- **Zipkin**
- **Elasticsearch**
- **Kibana**
- **Filebeat**
---

## Описание инфраструктуры

### 1. Kafka

- Кластер из **3 контроллеров** и **3 брокеров**
- Контроллеры слушают порты:
    - `9091`, `9092`, `9093`
- Брокеры слушают порты:
    - `9094`, `9095`, `9096`
- Логи пробрасываются из контейнера в папку:  
  `~/Universal_Trade_Platform/kafka/`

### 2. Kafka UI

- Веб-интерфейс для мониторинга очередей, подписчиков и отправителей Kafka
- Доступен локально:  
  [http://localhost:9090/](http://localhost:9090/)

### 3. Zipkin

- Веб-интерфейс для мониторинга распределённых запросов (tracing)
- Доступен локально:  
  [http://localhost:9411/](http://localhost:9411/)

### 4. Elasticsearch

- Хранилище логов и поисковый движок
- Работает в режиме **single-node**
- Java Heap Size: `1 GB`

### 5. Kibana

- Веб-интерфейс для поиска, визуализации и анализа логов
- Подключается к Elasticsearch по адресу:  
  `http://elasticsearch:9200`
- Доступен локально:  
  [http://localhost:5601/](http://localhost:5601/)

### 6. Filebeat

- Сборщик логов с Docker-контейнеров
- Подключается к:
    - `/var/lib/docker/containers`
    - `/var/run/docker.sock`
- Использует конфигурацию из файла:  
  `filebeat.docker.yml`

---

## 🚀 Запуск

Для создания общей сети внутри докер
```bash
if (-not (docker network inspect psup-shared-net -ErrorAction SilentlyContinue)) {docker network create psup-shared-net}
```

### Запуск Kafka и Kafka UI

```bash
docker-compose -f docker-compose-kafka.yml up
```

### Запуск Zipkin

```bash
docker-compose -f docker-compose-zipkin.yml up
```