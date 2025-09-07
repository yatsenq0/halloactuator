# 🚀 hello-actuator — Обучающее приложение с Spring Boot Actuator

> Простое, но мощное Spring Boot приложение, демонстрирующее возможности **Spring Boot Actuator** для мониторинга и управления приложением в реальном времени.

Этот проект — идеальная отправная точка для изучения **production-ready** возможностей Spring Boot.  
Он включает базовый REST-контроллер и включённый **Actuator**, что позволяет сразу увидеть, как выглядит работающее приложение с мониторингом.

---

## 📁 Структура проекта

```
src/
├── main/
│   ├── java/
│   │   └── com/example/helloactuator/
│   │       ├── HelloActuatorApplication.java
│   │       └── HelloController.java
│   └── resources/
│       └── application.properties
└── test/
    └── java/
        └── com/example/helloactuator/
            └── HelloActuatorApplicationTests.java
```

---

## 📄 Описание файлов

### `/src/main/java/com/example/helloactuator/HelloActuatorApplication.java`

Главная точка входа в приложение. Аннотация `@SpringBootApplication` включает автонастройку, сканирование компонентов и конфигурацию Spring MVC.

```java
package com.example.helloactuator;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class HelloActuatorApplication {
    public static void main(String[] args) {
        SpringApplication.run(HelloActuatorApplication.class, args);
    }
}
```

---

### `/src/main/java/com/example/helloactuator/HelloController.java`

Простой REST-контроллер, возвращающий текстовое сообщение по HTTP-запросу.

```java
package com.example.helloactuator;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Привет, Spring Boot! 🎉";
    }
}
```

> ✅ Проверьте: [http://localhost:8080/hello](http://localhost:8080/hello)

---

### `/src/main/resources/application.properties`

Конфигурационный файл, где включаются все Actuator-эндпоинты через HTTP.

```properties
# Включаем все Actuator-эндпоинты (только для обучения!)
management.endpoints.web.exposure.include=*

# Показывать детали статуса health
management.endpoint.health.show-details=always

# (Опционально) Добавьте информацию о приложении
# info.app.name=Hello Actuator App
# info.app.version=1.0.0
```

> ⚠️ **Внимание!**  
> В продакшене **никогда не используйте `*`** — указывайте только нужные эндпоинты, например: `health,info,metrics`.

---

### `/src/test/java/com/example/helloactuator/HelloActuatorApplicationTests.java`

Базовый тест, проверяющий, что контекст Spring успешно загружается.

```java
package com.example.helloactuator;

import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
class HelloActuatorApplicationTests {

    @Test
    void contextLoads() {
        // Проверка, что приложение корректно инициализируется
    }
}
```

---

## 🧩 Зависимости (`pom.xml`)

Проект использует следующие ключевые стартеры:

```xml
<dependencies>
    <!-- Веб-приложение -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <!-- Actuator для мониторинга и управления -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>

    <!-- Тестирование -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```

---

## 🚦 Доступные Actuator-эндпоинты

После запуска приложения откройте в браузере:

| Эндпоинт | Описание |
|--------|--------|
| 🔗 [http://localhost:8080/actuator](http://localhost:8080/actuator) | Список всех доступных эндпоинтов |
| 🟢 [http://localhost:8080/actuator/health](http://localhost:8080/actuator/health) | Статус работоспособности (`UP`/`DOWN`) |
| ℹ️ [http://localhost:8080/actuator/info](http://localhost:8080/actuator/info) | Информация о приложении (если задана в `application.properties`) |
| 📊 [http://localhost:8080/actuator/metrics](http://localhost:8080/actuator/metrics) | Доступные метрики (память, CPU, сессии и др.) |
| 🧩 [http://localhost:8080/actuator/beans](http://localhost:8080/actuator/beans) | Все Spring-бины в контексте |
| 🌐 [http://localhost:8080/actuator/env](http://localhost:8080/actuator/env) | Переменные окружения и свойства |
| 🧵 [http://localhost:8080/actuator/threaddump](http://localhost:8080/actuator/threaddump) | Состояние всех потоков |
| 🗑️ [http://localhost:8080/actuator/heapdump](http://localhost:8080/actuator/heapdump) | Снимок памяти (для анализа утечек) |

---

## 🚀 Как запустить

```bash
./mvnw spring-boot:run
```

Или:

```bash
./mvnw clean package
java -jar target/hello-actuator-0.0.1-SNAPSHOT.jar
```

---

## 📌 Что дальше?

1. 🔐 **Добавьте Spring Security**, чтобы защитить эндпоинты.
2. 📊 **Интегрируйте с Prometheus и Grafana** для визуализации метрик.
3. 🛠️ **Создайте кастомный эндпоинт** с помощью `@Endpoint`.
4. 🧪 **Добавьте кастомный `HealthIndicator`** для проверки БД или внешних сервисов.

---

## 📚 Источники

- [Spring Boot Actuator — TheServerSide](https://www.theserverside.com/video/Spring-Boot-Actuator-tutorial)
- [Comprehensive Guide to Spring Boot Actuator — Medium](https://medium.com/@pratik.941/a-comprehensive-guide-to-spring-boot-actuator-c2bd63a32ede)
- [Actuator Service Guide — spring.io](https://spring.io/guides/gs/actuator-service)

---

## 💡 Зачем это нужно?

> _"The Spring Boot Actuator is the one Spring starter that I recommend every developer add to their Gradle build or Maven POM file."_  
> — **Cameron McKenzie**, Java EE engineer

Actuator превращает ваше приложение в **самоуправляющуюся систему**, способную сообщать о своём состоянии, производительности и проблемах — критически важно для DevOps, Kubernetes и production-сред.

---

## ✅ Вывод

Этот проект — ваш **первый шаг к production-ready Spring Boot приложениям**.  
Теперь вы знаете, как быстро добавить мониторинг, увидеть состояние приложения и подготовить его к реальным нагрузкам.
```

---


