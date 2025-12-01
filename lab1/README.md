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

### 1. Создание Service Account

Создан service account с именем `vtantsiura-sa-lab1` в проекте `cloud-platforms-as-the-basis`. Service account имеет email:
```
vtantsiura-sa-lab1@cloud-platforms-as-the-basis.iam.gserviceaccount.com
```

![telegram-cloud-photo-size-2-5291816239355334172-y](https://github.com/user-attachments/assets/b8677e8b-649c-4b35-9aad-01a654e345d1)

*Создание service account vtantsiura-sa-lab1 в Google Cloud Console.*

### 2. Создание виртуальной машины в Google Cloud Platform

Была создана виртуальная машина `vtantsiura-vm-lab1` в зоне `us-central1-c` проекта `cloud-platforms-as-the-basis`. VM имеет:
- Внутренний IP: `10.128.0.57 (nic0)`
- Внешний IP: `34.69.245.171 (nic0)`
- Статус: запущена (зеленая галочка)

![telegram-cloud-photo-size-2-5291816239355334182-y](https://github.com/user-attachments/assets/b0100e99-73f4-47c8-bf65-6ff4f0b73690)

*Список VM instances в Google Cloud Console. Видна созданная VM vtantsiura-vm-lab1 со статусом "Running".*

### 3. Подключение к VM через SSH

Выполнено подключение к виртуальной машине через SSH-in-browser интерфейс Google Cloud Platform. Пользователь: `tanzuraseva@vtantsiura-vm-lab1`.

![telegram-cloud-photo-size-2-5291816239355334185-y](https://github.com/user-attachments/assets/b22b8638-f25b-463c-80e6-f797e2116ac3)

*Подключение к VM через SSH-in-browser интерфейс Google Cloud Platform.*

### 4. Работа с Google Cloud Storage

#### 4.1. Просмотр содержимого bucket

Выполнена команда для просмотра содержимого bucket `lab1-bucket-itmo`:
```bash
gsutil ls gs://lab1-bucket-itmo/
```

Результат: в bucket находятся три изображения:
- `pic1.jpg`
- `pic2.jpg`
- `pic3.jpeg`

![telegram-cloud-photo-size-2-5291816239355334195-y](https://github.com/user-attachments/assets/0058e682-dd60-4b2f-8fb7-9dcfee5fd8a0)

*Просмотр содержимого bucket с помощью команды gsutil ls.*

#### 4.2. Копирование файлов из bucket

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

![telegram-cloud-photo-size-2-5291816239355334195-y](https://github.com/user-attachments/assets/5cc7fd99-106e-4117-94f4-46643a9dc7a3)

*Копирование файлов из bucket на локальную машину и проверка результата командой ls -lah.*

### 5. Настройка IAM permissions

Service account `vtantsiura-sa-lab1` был добавлен в IAM с ролью `Compute Viewer`. Это позволяет service account просматривать ресурсы Compute Engine, но не дает полных прав доступа.

![telegram-cloud-photo-size-2-5291816239355334201-y](https://github.com/user-attachments/assets/32a296e3-ddec-453a-94b2-a0e3e5d30b72)

*Настройка IAM permissions для service account. Видно, что vtantsiura-sa-lab1 имеет роль Compute Viewer.*


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

![telegram-cloud-photo-size-2-5291816239355334204-y](https://github.com/user-attachments/assets/a44074db-2666-425e-a9d5-0a46f79a30d2)

*Ошибка доступа при попытке выполнить команду gsutil cp без указания destination. Service account не имеет прав storage.objects.list.*

## Выводы

В ходе лабораторной работы были выполнены следующие задачи:
1. ✅ Создан service account в Google Cloud Platform
2. ✅ Создана виртуальная машина в Google Cloud Platform
3. ✅ Выполнено подключение через SSH
4. ✅ Изучена работа с Google Cloud Storage через утилиту `gsutil`
5. ✅ Успешно скопированы файлы из bucket на локальную машину
6. ✅ Настроены базовые IAM permissions
7. ✅ Выявлена проблема с правами доступа service account к Storage bucket

Работа продемонстрировала базовые навыки работы с Google Cloud Platform, включая управление виртуальными машинами, работу с облачным хранилищем и настройку прав доступа через IAM.

