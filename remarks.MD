## 1. Источники текстовых данных новостей и социальных постов по крипте

### Основные источники:
- **Новости**: 
  - Криптовалютные новостные сайты: CoinDesk, CoinTelegraph, Decrypt, The Block, Bitcoin Magazine.
- **Социальные посты**: 
  - Twitter (X), Reddit (r/cryptocurrency, r/bitcoin и т.д.), группы в Telegram, серверы на Discord, публичные форумы (например, Bitcointalk).
- **Альтернативные источники**: 
  - Блоги на Medium, видео на YouTube.

### Как получал бы данные?
- **Новости**: 
  - Использую RSS-каналы, веб-скрейпинг или API от новостных источников (CoinGecko, CryptoCompare).
- **Социальные посты**:
  - **Twitter (X)**: Официальное API Twitter (v2).
  - **Reddit**: Reddit API (через PRAW или прямые HTTP-запросы).
  - **Telegram/Discord**: Публичные боты или API для скрейпинга открытых групп/каналов.
  - **Форумы**: Веб-скрейпинг (например, Bitcointalk) с использованием BeautifulSoup или Scrapy.

### Как бы организовал сбор данных?
- **Конвейер данных**:
  - Определяю релевантные ключевые слова ("Bitcoin", "Ethereum", "DeFi", и т.д.).
  - Использую API или скрейперы для получения данных ежедневно или в реальном времени.
  - Сохраняю данные в БД (PostgreSQL/MongoDB) или в data lake (AWS S3).
  - Использую системы очередей (RabbitMQ, Kafka) для управления сбором и обработкой данных.
- **Предобработка**: 
  - Очищаю и дедуплицирую данные, удаляю спам, нормализую текст.

### Какие библиотеки использовать?
- **API и скрейпинг**:
  - requests, BeautifulSoup, Scrapy, selenium (для страниц с JavaScript).
  - tweepy или snscrape для Twitter, PRAW для Reddit, telethon для Telegram.
- **Хранение данных**:
  - pandas, sqlalchemy, pymongo.
- **Конвейер данных**:
  - Apache Airflow, Luigi, Prefect.
- **Обработка естественного языка (по желанию)**:
  - spaCy, NLTK, transformers.


## 2. Работа с незнакомыми данными

Нередко сталкивался с неструктурированными данными:
- **Легаси-логи**: Работал с логами приложений, системными логами, часто с устаревшими или нестандартными форматами, где были пропущены метки времени или отсутствовала структура.
- **Неструктурированные CSV**: Сталкивался с CSV-файлами без заголовков, с несоответствующими столбцами, перемешанными типами данных и различными разделителями. Иногда внутри были вложенные JSON или XML.
- **Неструктурированные JSON**: Работал с сильно вложенными или неконсистентными JSON, например, с данных от API или сторонних сервисов с плохой документацией.

---

### Методы для быстрого понимания смысла и сути незнакомых данных

1. **Начальная проверка данных**:
   - Загружаю данные в pandas и использую функции `df.head()`, `df.info()` для первых наблюдений.
   - Для больших файлов использую инструменты командной строки: `head`, `tail`, `grep` для поиска паттернов.

2. **Анализ структуры**:
   - Для логов: извлекаю повторяющиеся паттерны с помощью регулярных выражений или инструментов вроде `loguru`.
   - Для JSON: использую `json.dumps()` с отступами или `pandas.json_normalize()` для «распаковки» вложенных объектов.
   - Для CSV: проверяю разделители и кодировку с помощью `csv`, `file`, `iconv`.

3. **Очистка и сводка данных**:
   - Выявляю пропущенные значения (`df.isnull().sum()`), дубликаты (`df.duplicated()`), аномалии с помощью `df.describe()`.
   - Использую визуализацию (гистограммы, диаграммы) с помощью `seaborn`, `matplotlib` и `plotly` для поиска трендов и выбросов.

4. **Итеративное понимание**:
   - Тестирую гипотезы, фильтруя данные по ключевым словам или кодам ошибок.
   - Группирую данные по типам ошибок или частоте ключей в JSON.

5. **Документация или реверс-инжиниринг**:
   - Если доступна документация, использую её. Если нет — создаю собственные заметки и документирую структуру для будущей работы.

---

### Используемые библиотеки:
- **Для анализа данных**: pandas, numpy, csv, json, jq, loguru.
- **Для парсинга/предобработки**: re (регулярные выражения), pandas.json_normalize, awk, sed.
- **Для визуализации**: matplotlib, seaborn, plotly.
- **Для логов**: loguru, ELK Stack (Elasticsearch, Logstash, Kibana) для масштабного анализа логов.

---

## 3. ML-стек

### Опыт с фреймворками и инструментами

#### 1. (Big) Data wrangling, processing, and visualization
- Pandas
- Parquete
- DVC
- Numba
- Spark
- Hadoop
- Hive
- HDFS
- Cassandra
- Plotly
- Seaborn
- Matplotlib
- Datasets
- Sklearn

#### 2. Model Training / Efficient ML
- Horovod
- Hivemind
- DeepSpeed
- Torch Distributed
- Qdrant
- Sklearn
- CatBoost, LightGBM
- Langchain / LangGraph
- HuggingFace Transformers, Sentence Transformers
- Accelerate
- PyTorch
- Optuna
- ONNX

#### 3. Experiments, monitoring, inference
- Airflow
- MLflow
- Weights & Biases
- Hydra
- ONNX Runtime
- bitsandbytes
- TensorFlow Serving, NVIDIA Triton
- Grafana
- Prometheus
- ELK (Elastic, Logstash, Kibana)

### Протокол построения пайплайна

1. **Сбор данных**:  
   - Использую DVC, Spark, Hadoop для обработки больших данных.  
   - Cassandra/Hive/HDFS для хранения.  

2. **Предобработка и анализ**:  
   - Pandas, Sklearn, Numba для трансформации и визуализации (Seaborn, Matplotlib, Plotly).  
   - Parquet как альтернатива Pandas для работы с большим количеством данных.

3. **Моделирование и тренировка**:  
   - PyTorch, HuggingFace, CatBoost, LightGBM для модели.  
   - Horovod, DeepSpeed, Torch Distributed, Hivemind для распределенного обучения.

4. **Мониторинг и деплой**:  
   - Airflow, MLflow, Weights & Biases для трекинга и оркестрации.  
   - TensorFlow Serving, NVIDIA Triton, ONNX Runtime для инференса.  
   - Prometheus, Grafana для мониторинга.

5. **Автоматизация**:  
   - Использую Hydra для конфигураций и оптимизаций.

