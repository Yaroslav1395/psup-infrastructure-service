# PSUP-INFRASTRUCTURE_SERVICE

**PSUP-INFRASTRUCTURE_SERVICE** — сервис для запуска инфраструктуры универсальной платформы по дистрибуции товаров.

---

## Инфраструктура

- **Kafka** (в режиме KRaft)
- **Kafka UI**
- **Zookeeper**
---

## Описание инфраструктуры

### 1. Kafka

- Кластер из **3 контроллеров** и **3 брокеров**
- Контроллеры слушают порты:  
  `9091`, `9092`, `9093`
- Брокеры слушают порты:  
  `9094`, `9095`, `9096`
- Логи пробрасываются из контейнера в папку:  
  `~/Universal_Trade_Platform/kafka/`

### 2. Kafka UI

- Веб-интерфейс для мониторинга очередей, подписчиков и отправителей Kafka
- Доступен локально по адресу:  
  [http://localhost:9090/](http://localhost:9090/)

### 3. Zipkin
- Веб-интерфейс для мониторинга запросов
- Доступен локально по адресу:  
    [http://localhost:9411/](http://localhost:9411/)
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