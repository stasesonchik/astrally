# Диаграммы Astrally

## Диаграмма последовательности

Диаграмма показывает основной сценарий получения ответа в мистическом чате.

```mermaid
sequenceDiagram
    actor User as Пользователь
    participant Web as Веб-интерфейс
    participant API as Backend API
    participant Context as Сервис контекста
    participant LLM as Языковая модель

    User->>Web: Вводит и отправляет вопрос
    Web->>API: Передаёт вопрос и настройки
    API->>Context: Запрашивает разрешённый контекст

    alt Персонализация разрешена
        Context-->>API: Профиль и релевантная история
    else Персонализация отключена
        Context-->>API: Пустой контекст
    end

    API->>LLM: Передаёт вопрос, стиль и контекст
    LLM-->>API: Возвращает интерпретацию
    API-->>Web: Возвращает ответ и предупреждение
    Web-->>User: Показывает ответ
```

## Диаграмма классов

Диаграмма отражает основные сущности первой версии сервиса. Технические классы интеграции с языковой моделью здесь не показаны, чтобы диаграмма оставалась простой и описывала предметную область.

```mermaid
classDiagram
    class User {
        +int id
        +string email
        +bool personalizationEnabled
        +deletePersonalData()
    }

    class MysticProfile {
        +int id
        +string nickname
        +date birthDate
        +string[] interests
        +updateProfile()
    }

    class Conversation {
        +int id
        +datetime createdAt
        +string mysticalStyle
        +addMessage()
    }

    class Message {
        +int id
        +string role
        +string content
        +datetime createdAt
    }

    class TarotReading {
        +int id
        +string topic
        +string[] cards
        +string interpretation
        +datetime createdAt
    }

    User "1" --> "0..1" MysticProfile : заполняет
    User "1" --> "0..*" Conversation : ведёт
    Conversation "1" *-- "1..*" Message : содержит
    User "1" --> "0..*" TarotReading : выполняет
```
