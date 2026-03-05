<p align="center">

# ⚡ MiniRedis

### A Lightweight Redis-Inspired In-Memory Cache Engine built with .NET

High-performance key-value storage, TTL expiration, eviction strategies, Pub/Sub system and real-time monitoring dashboard.

</p>

<p align="center">

![.NET](https://img.shields.io/badge/.NET-8-purple)
![ASP.NET](https://img.shields.io/badge/ASP.NET-Core-blue)
![Next.js](https://img.shields.io/badge/Next.js-Frontend-black)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-in%20development-orange)

</p>

---

# 🧠 About The Project

**MiniRedis** — это учебный backend-проект, в котором реализуется **in-memory cache engine**, вдохновлённый архитектурой Redis.

Основная цель проекта — **глубоко понять архитектуру высокопроизводительных backend-систем**.

Внутри проекта реализованы:

- потокобезопасное хранилище
- TTL expiration
- алгоритмы вытеснения
- Pub/Sub система
- real-time мониторинг
- административная панель

Проект разделён на две части:

| Component | Description |
|---|---|
Backend | ASP.NET Core cache engine |
Frontend | Next.js Admin Dashboard |

---

# ✨ Features

### ⚡ High Performance In-Memory Storage

Потокобезопасное хранилище ключ-значение.

Поддерживаемые команды:

```text
SET key value
GET key
DEL key
```

# ⏳ TTL Expiration
Каждый ключ может иметь время жизни.
```text
SET session:1 "active" EX 60
```
Через 60 секунд ключ автоматически удалится.

----

# 🧠 Memory Eviction Strategies
Когда кэш достигает лимита, запускается политика вытеснения.

| Strategy | Description |
|---|---|
LRU | Least Recently Used |
FIFO | First In First Out |

----

# 📡 Pub/Sub Messaging
Система обмена событиями между клиентами.

```text
SUBSCRIBE notifications
PUBLISH notifications "New user registered"
```

Используется **Observer Pattern**.

----

# 📊 Real-Time Monitoring
Админ-панель отображает:

- Cache Hits / Misses

- количество ключей

- использование памяти

- TTL cleanup events

- Pub/Sub события

Все данные приходят в реальном времени через **WebSockets**.

----

# 🏗 System Architecture

```
              +----------------------+
              |     Next.js Admin    |
              |       Dashboard      |
              +----------+-----------+
                         |
                      WebSocket
                         |
+------------------------------------------------+
|              ASP.NET Core Backend              |
|                                                |
|  Controllers                                   |
|      |                                         |
|      v                                         |
|  Cache Engine (Singleton)                      |
|      |                                         |
|      +-------------------------+               |
|      |                         |               |
| ConcurrentDictionary      Eviction Strategy    |
|      |                         |               |
|      v                         v               |
|   CacheEntry              LRU / FIFO           |
|                                                |
| Background Worker                              |
| TTL Expiration Cleaner                         |
+------------------------------------------------+
```

----

# 🧩 Design Patterns
***Strategy Pattern***
Используется для выбора политики вытеснения.

```text
IEvictionStrategy
 ├── LruStrategy
 └── FifoStrategy
```

***Observer Pattern***
Используется для Pub/Sub системы.

```
Publisher
   |
   +--- Channel
           |
           +--- Subscribers
```

***Factory Pattern***
Преобразует текстовые команды в объекты.

```text
SET key value EX 60
```
↓
```text
ICommand
```

----

# 🧠 Core Data Structures
**ConcurrentDictionary**
Основное хранилище:
```text
ConcurrentDictionary<string, CacheEntry>
```

***Преимущества:***

- потокобезопасность

- высокая производительность

- минимальные блокировки

---

**CacheEntry**
Каждая запись хранит:
```text
Key
Value
CreatedAt
TTL
LastAccessTime
```

***Это позволяет реализовать:***

- TTL expiration

- LRU

- метрики использования

-----

# ⚙ Background Workers
---
Фоновый сервис реализован через:

```text
IHostedService
```

***Worker:***

- периодически просыпается

- проверяет ключи

- удаляет истёкшие TTL

Будущая оптимизация:

```text
Min Heap (priority queue)
```

----

# 📊 Admin Dashboard
Frontend реализован на Next.js.

***Dashboard***
Отображает:

- Cache Hits

- Cache Misses

- количество ключей

- использование памяти

- события TTL

---

***Key Explorer***
Просмотр всех ключей.

| **Key** |	**Value**	| **TTL** |
|---|---|---|

***Можно:***

- создать ключ

- изменить

- удалить

----

# Console
Терминал для отправки команд:

```text
GET user:1
SET counter 100
DEL session:42
```
----

# 📂 Project Structure
```text
MiniRedis
│
├── backend
│   ├── API
│   ├── Core
│   ├── Eviction
│   ├── Commands
│   └── Workers
│
└── frontend
    └── nextjs-dashboard
```

----

# 🚀 Getting Started
***Clone repository***
**Bash**
```text
git clone https://github.com/aleexxeyy/RedisProject )
```

***Run Backend***
**Bash**
```text
cd backend
dotnet run
```

**API будет доступно:**
```text
http://localhost:5000
```
----

***Run Frontend***
***Bash**
```text
cd frontend
npm install
npm run dev
```
**Админка:**
```text
http://localhost:3000
```
----

# 🎯 Learning Goals
**MiniRedis** создан для изучения:

- архитектуры cache систем

- потокобезопасных структур данных

- backend design patterns

- real-time систем

Проект вдохновлён Redis, но **реализован полностью самостоятельно для обучения**.
----

⭐ Support
Если проект оказался полезным — поставь ⭐ репозиторию.
