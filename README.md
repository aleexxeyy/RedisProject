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

```
SET key value
GET key
DEL key
```

---

### ⏳ TTL Expiration

Каждый ключ может иметь время жизни.

```
SET session:1 "active" EX 60
```

Через 60 секунд ключ автоматически удалится.

---

### 🧠 Memory Eviction Strategies

Когда кэш достигает лимита, запускается политика вытеснения.

| Strategy | Description |
|---|---|
LRU | Least Recently Used |
FIFO | First In First Out |

---

### 📡 Pub/Sub Messaging

Система обмена событиями между клиентами.

```
SUBSCRIBE notifications
PUBLISH notifications "New user registered"
```

Используется **Observer Pattern**.

---

### 📊 Real-Time Monitoring

Админ-панель отображает:

- Cache Hits / Misses
- количество ключей
- использование памяти
- TTL cleanup events
- Pub/Sub события

Все данные приходят **в реальном времени через WebSockets**.

---

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
| ConcurrentDictionary      Eviction Strategy   |
|      |                         |               |
|      v                         v               |
|   CacheEntry             LRU / FIFO            |
|                                                |
| Background Worker                              |
| TTL Expiration Cleaner                         |
+------------------------------------------------+
```

---

# 🧩 Design Patterns

### Strategy Pattern

Используется для выбора политики вытеснения.

```
IEvictionStrategy
 ├── LruStrategy
 └── FifoStrategy
```

Позволяет легко добавлять новые алгоритмы.

---

### Observer Pattern

Используется для Pub/Sub системы.

```
Publisher
   |
   +--- Channel
           |
           +--- Subscribers
```

---

### Factory Pattern

Преобразует текстовые команды в объекты.

```
SET key value EX 60
```

↓

```
ICommand
```

---

# 🧠 Core Data Structures

## ConcurrentDictionary

Основное хранилище:

```
ConcurrentDictionary<string, CacheEntry>
```

Преимущества:

- потокобезопасность
- высокая производительность
- минимальные блокировки

---

## CacheEntry

Каждая запись хранит:

```
Key
Value
CreatedAt
TTL
LastAccessTime
```

Это позволяет реализовать:

- TTL expiration
- LRU
- метрики использования

---

# ⚙ Background Workers

Фоновый сервис реализован через:

```
IHostedService
```

Worker:

1. периодически просыпается
2. проверяет ключи
3. удаляет истёкшие TTL

Будущая оптимизация:

```
Min Heap (priority queue)
```

---

# 📊 Admin Dashboard

Frontend реализован на **Next.js**.

### Dashboard

Отображает:

- Cache Hits
- Cache Misses
- количество ключей
- использование памяти
- события TTL

---

### Key Explorer

Просмотр всех ключей.

| Key | Value | TTL |
|---|---|---|

Можно:

- создать ключ
- изменить
- удалить

---

### Console

Терминал для отправки команд:

```
GET user:1
SET counter 100
DEL session:42
```

---

### Pub/Sub Tester

Позволяет тестировать события в реальном времени.

---

# 📸 Screenshots

## Admin Dashboard

```
(Добавь сюда скриншот админки)

docs/images/dashboard.png
```

---

## Key Explorer

```
docs/images/key-explorer.png
```

---

## Console

```
docs/images/console.png
```

---

# 📂 Project Structure

```
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

---

# 🚀 Getting Started

## Clone repository

```
git clone https://github.com/yourusername/miniredis
```

---

## Run Backend

```
cd backend
dotnet run
```

API будет доступно:

```
http://localhost:5000
```

---

## Run Frontend

```
cd frontend
npm install
npm run dev
```

Админка:

```
http://localhost:3000
```

---

# 📈 Roadmap

### v1

- [x] Cache Engine
- [x] SET / GET / DEL
- [x] TTL

### v2

- [ ] LRU eviction
- [ ] FIFO eviction
- [ ] metrics

### v3

- [ ] Pub/Sub
- [ ] WebSocket streaming
- [ ] Admin Dashboard

### v4

- [ ] Persistence
- [ ] Cluster mode
- [ ] Sharding

---

# 🎯 Learning Goals

MiniRedis создан для изучения:

- архитектуры cache систем
- потокобезопасных структур данных
- backend design patterns
- real-time систем

Проект вдохновлён Redis, но **реализован полностью самостоятельно для обучения**.

---

# ⭐ Support

Если проект оказался полезным — поставь ⭐ репозиторию.
