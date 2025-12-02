# Lab2 Report

**University:** ITMO University

**Faculty:** FICT

**Course:** Cloud platforms as the basis of technology entrepreneurship

**Year:** 2025/2026

**Group:** U4225

**Author:** Tantsiura Valentin Olegovich

**Lab:** Lab2

**Date of create:** 02.12.2025

**Date of finished:** 02.12.2025

## Ход работы: Google Cloud Run

### 1. Создание сервиса

В консоли Google Cloud был создан сервис Cloud Run на основе демонстрационного образа hello. В настройках выбраны минимальные ресурсы (256 MiB RAM, 1 CPU) и разрешены неаутентифицированные вызовы (Allow unauthenticated invocations), чтобы сервис был доступен из интернета.

![telegram-cloud-photo-size-2-5294068039169019565-y](https://github.com/user-attachments/assets/5dd8cd05-4fe3-4d80-85aa-caafab819bfb)

### 2. Тестирование сервиса

Выполнен переход по сгенерированной ссылке (.run.app). Сервис успешно обрабатывает запросы, отображается стартовая страница приветствия.

![telegram-cloud-photo-size-2-5294068039169019568-y](https://github.com/user-attachments/assets/5252fedc-a7b6-4e0d-b5d4-9ad02871f934)

### 3. Анализ метрик и логов

В разделе Metrics проанализированы графики количества запросов (Request count) и использования процессора контейнером. В разделе Logs зафиксированы записи об успешном запуске контейнера и обработке входящих HTTP-запросов (код 200).

![telegram-cloud-photo-size-2-5294068039169019570-y](https://github.com/user-attachments/assets/24f25340-746c-4f1f-bd67-9e48e57029c2)


![telegram-cloud-photo-size-2-5294068039169019571-y](https://github.com/user-attachments/assets/6edd5c9f-760c-41c7-8db3-8dc18560c521)

### 4. Изменение конфигурации (Смена порта)

Создана новая ревизия сервиса: порт контейнера изменен со стандартного 8080 на 8090. Приложение успешно развернулось и продолжило работу, так как образ поддерживает динамическое назначение порта через переменную окружения $PORT. Ошибок (502/503) не возникло.

### 5. Управление трафиком (Traffic Splitting)

Настроено разделение трафика между ревизиями: 50% запросов направляется на старую версию (порт 8080), 50% — на новую (порт 8090). При многократном обновлении страницы запросы распределяются между версиями сервиса.

![telegram-cloud-photo-size-2-5294068039169019597-y](https://github.com/user-attachments/assets/b3ce22dd-5954-4103-a860-a2c1b19d2798)

### 6. Удаление ресурсов

Все созданные сервисы Cloud Run были удалены для освобождения ресурсов.

[ВСТАВИТЬ СКРИНШОТ: ПУСТОЙ СПИСОК СЕРВИСОВ ИЛИ ПРОЦЕСС УДАЛЕНИЯ]

