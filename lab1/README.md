# Lab0 Report

University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [Cloud platforms as the basis of technology entrepreneurship](https://)

Year: 2025/2026

Group: U4225

Author: Tantsiura Valentin Olegovich

Lab: Lab0

Date of create: 02.12.2025

Date of finished: 02.12.2025

## Описание выполненной работы

### 1. Создание виртуальной машины в Google Cloud Platform

Была создана виртуальная машина `vtantsiura-vm-lab1` в зоне `us-central1-c` проекта `cloud-platforms-as-the-basis`. VM имеет:
- Внутренний IP: `10.128.0.57 (nic0)`
- Внешний IP: `34.69.245.171 (nic0)`
- Статус: запущена (зеленая галочка)

### 2. Подключение к VM через SSH

Выполнено подключение к виртуальной машине через SSH-in-browser интерфейс Google Cloud Platform. Пользователь: `tanzuraseva@vtantsiura-vm-lab1`.

### 3. Работа с Google Cloud Storage

#### 3.1. Просмотр содержимого bucket

Выполнена команда для просмотра содержимого bucket `lab1-bucket-itmo`:
```bash
gsutil ls gs://lab1-bucket-itmo/
```

Результат: в bucket находятся три изображения:
- `pic1.jpg`
- `pic2.jpg`
- `pic3.jpeg`

#### 3.2. Копирование файлов из bucket

Успешно скопированы все три файла из bucket на локальную машину:
```bash
gsutil cp gs://lab1-bucket-itmo/pic1.jpg .
gsutil cp gs://lab1-bucket-itmo/pic2.jpg .
gsutil cp gs://lab1-bucket-itmo/pic3.jpeg .
```

Результаты копирования:
- `pic1.jpg`: 227.8 KiB
- `pic2.jpg`: 486.6 KiB
- `pic3.jpeg`: 857.9 KiB

Все файлы успешно загружены в домашнюю директорию пользователя.

### 4. Создание Service Account

Создан service account с именем `vtantsiura-sa-lab1` в проекте `cloud-platforms-as-the-basis`. Service account имеет email:
```
vtantsiura-sa-lab1@cloud-platforms-as-the-basis.iam.gserviceaccount.com
```

### 5. Настройка IAM permissions

Service account `vtantsiura-sa-lab1` был добавлен в IAM с ролью `Compute Viewer`. Это позволяет service account просматривать ресурсы Compute Engine, но не дает полных прав доступа.

### 6. Проблема с доступом к Storage

При попытке выполнить команду без указания destination:
```bash
gsutil cp gs://lab1-bucket-itmo/pic1.jpg
```

Возникла ошибка доступа:
```
AccessDeniedException: 403 vtantsiura-sa-lab1@cloud-platforms-as-the-basis.iam.gserviceaccount.com does not have storage.objects.list access to the Google Cloud Storage bucket. Permission 'storage.objects.list' denied on resource (or it may not exist).
```

Это указывает на то, что service account, используемый VM, не имеет необходимых прав для работы с Google Cloud Storage bucket. Для решения этой проблемы необходимо добавить роль `Storage Object Viewer` или `Storage Admin` для service account.

## Выводы

В ходе лабораторной работы были выполнены следующие задачи:
1. ✅ Создана виртуальная машина в Google Cloud Platform
2. ✅ Выполнено подключение через SSH
3. ✅ Изучена работа с Google Cloud Storage через утилиту `gsutil`
4. ✅ Успешно скопированы файлы из bucket на локальную машину
5. ✅ Создан service account
6. ✅ Настроены базовые IAM permissions
7. ✅ Выявлена проблема с правами доступа service account к Storage bucket

Работа продемонстрировала базовые навыки работы с Google Cloud Platform, включая управление виртуальными машинами, работу с облачным хранилищем и настройку прав доступа через IAM.

