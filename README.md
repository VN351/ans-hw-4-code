# Ansible Playbook для установки ClickHouse и Vector

## Содержание
- [Обзор](#обзор)
- [Особенности](#особенности)
- [Требования](#требования)
- [Структура директорий](#структура-директорий)
- [Использование](#использование)


## Обзор

Этот Ansible playbook при использовании ролей устанавливает и настраивает **ClickHouse**, **Vector** и **Lighthouse** на указанных хостах. Он упрощает процесс развертывания, обеспечивая консистентную и эффективную установку обоих сервисов в вашей инфраструктуре.

## Особенности

- **Установка ClickHouse:**
  - Скачивает и устанавливает RPM-пакеты ClickHouse.
  - Создает необходимую базу данных ClickHouse.
  - Управляет сервисом ClickHouse.

- **Установка Lighthouse:**
  - Устанавливает и настраивает Nginx.
  - Клонирует репозиторий приложения в необходимую директорию.
  - Применяет пользовательские конфигурации Nginx и Lighthouse.
  - Управляет сервисом Lighthouse.
  
- **Установка Vector:**
  - Скачивает и устанавливает RPM-пакеты Vector.
  - Применяет пользовательские конфигурации Vector через шаблоны.
  - Управляет сервисом Vector.

## Требования

- **Ansible:** Версия 2.9 или выше.
- **Управляемые хосты:**
  - Операционная система: Совместима с дистрибутивами на основе RPM (например, CentOS, RHEL, Fedora).
  - Менеджер пакетов: Должен быть доступен yum.
- **Сетевой доступ:**
  - Возможность скачивания пакетов с внешних URL.
  - SSH-доступ к управляемым хостам.

## Структура директорий
  ```
  ans-hw-4-code/
  ├── inventory/
  │   └── prod.yml
  ├── requirements.yml
  ├── site.yml
  └── README.md
  ```
- **site.yml:** Основной playbook, содержащий все задачи установки.
- **requirements.yml:** Скачивает необзодимые роли.
- **inventory/prod.yml:** Inventoty файл.


## Использование

1. **Клонируйте репозиторий:**
    ```bash
    git clone https://github.com/VN351/ans-hw-4-code.git
    cd ans-hw-4-code
    ```
2. **Настройте инвентарь:**
   Отредактируйте файл templates/prod.yml, добавив ваши хосты ClickHouse, Vector и Lighthouse.
   **Пример templates/prod.yml:**
    ```yml
    ---
    clickhouse:
      hosts:
        clickhouse-01:
          ansible_host: 51.250.0.122
          ansible_user: fedora
    vector:
      hosts:
        vector-01:
          ansible_host: 89.169.131.240
          ansible_user: fedora
    lighthouse:
      hosts:
        lighthouse-01:
          ansible_host: 158.160.52.165
          ansible_user: fedora
    ```
3. **Запустите Playbook:**
    ```bash
    ansible-playbook -i templates/prod.yml site.yml
    ```  


