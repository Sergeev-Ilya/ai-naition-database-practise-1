# ADR-001: Технологический стек справочника контактов

**Статус:** принят

## Контекст

Нужны простой UI, REST API на Java, атомарная защита от дублей, хранение от 1 млн записей и поиск с p99 до 20 мс при 100 RPS.

## Решение

| Компонент | Технология | Почему и плюсы |
|---|---|---|
| UI | HTML5, CSS3, JavaScript без фреймворка | Форма простая; не нужны React/Vue и Node.js-сборка. Быстрая загрузка, мало зависимостей. Статика поставляется тем же Spring Boot-приложением. |
| REST-приложение | Java 25 LTS (Eclipse Temurin), Spring Boot 3.5.x, Spring MVC, Bean Validation, Spring Data JDBC, Maven | Соответствует требованию Java. Spring Boot ускоряет создание REST API и дает готовые валидацию, транзакции, health checks и метрики. Spring Data JDBC проще JPA для одной таблицы и дает предсказуемый SQL. |
| СУБД | PostgreSQL 18, миграции Flyway | ACID-транзакции обеспечивают сохранность; составной UNIQUE-индекс атомарно блокирует дубли; B-tree индексы по нормализованным имени и телефону ускоряют точный поиск. PostgreSQL открыт и рассчитан на объем существенно больше 1 млн строк. |

## Последствия

- UI и API собираются и разворачиваются одним приложением.
- PostgreSQL запускается отдельным сервисом; схема версионируется Flyway.
- SLA 20/50 мс подтверждается нагрузочными тестами: сам выбор технологий его не гарантирует.
- SPA-фреймворк добавляется только при существенном усложнении интерфейса.

## Источники

- [Spring Boot 3.5 — системные требования](https://docs.spring.io/spring-boot/3.5/system-requirements.html)
- [Spring Boot — REST и статические ресурсы](https://docs.spring.io/spring-boot/3.3/reference/web/servlet.html)
- [PostgreSQL — уникальные ограничения](https://www.postgresql.org/docs/current/ddl-constraints.html)
- [Eclipse Temurin — поддержка LTS](https://adoptium.net/support/)
