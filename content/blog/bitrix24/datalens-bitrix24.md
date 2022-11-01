---
title: "Настройка Yandex DataLens Битрикс24"
date: 2022-10-02T13:32:41+03:00
draft: true
slug: ""
description: ""
keywords: [Bitrix24,Yandex-DataLens,Integration,Настройка Битрикс24,Интеграция]
tags: [Bitrix24,Yandex-DataLens,Integration]        
math: false
toc: true
---

<h2>Настройка интеграции Yandex DataLens и Битрикс24</h2>

### 1. Получить токен для подключения Битрикс24 к DataLens.<br>
1. **Перейти в раздел CRM - Аналитика - BI-аналитика**, в правой части страницы будет информация для подключения 

```DataConnect
     Адрес сервера - адрес вашего портала Битрикс24.
     Секретный ключ 
```
![bi-connect](/images/datalens-bitrix24/bitrix24-connect.png)


### 2. Настройка подключения в сервисе DataLens для получения данных из Битрикс24 <br>
1. Перейдем в сервис [Yandex DataLens](https://datalens.yandex.ru).
2. Создадим новое подключение, используя блок подключений кликнув по кнопке "Создать подключение".
![datalens-connect](/images/datalens-bitrix24/datalens-connect.png)<br>
3. Из списка доступных сервисов, выбираем **Битрикс24**
![select-bitrix24](/images/datalens-bitrix24/select-bitrix24.png)<br>
4. В форме добавления информации для подключению (полученных в п.1) к вашему Битрикс24, параметр **"Автоматически создать дашборд, чарты и датасет над подключением"** устанавливаем.<br>
![datalens-connect-B24](/images/datalens-bitrix24/datalens-connect-B24.png)<br>
5. Для проверки корректности указанных данных в форме, можно нажав кнопку **"Проверить подключение"**, если данные указаны верно рядом с кнопкой будет отображена иконка успешного подключения<br>
![check-connect](/images/datalens-bitrix24/check-connect.png)
6. Для сохранения настроек нажимаем кнопку **"Создать подключение"**, и указываем директорию для хранения и имя подключения
![connect-name](/images/datalens-bitrix24/name-connect.png)
   

### 3. Настройка датасетов в DataLens
1. При уставленном параметре **"Автоматически создать дашборд, чарты и датасет над подключением"** будут созданы стандартные чарты и датасеты, которые можно использовать.
![datalens-lists](/images/datalens-bitrix24/datalens-lists.png)
   
2. Создадим датасет который будем использовать в нашем будущем чарте.
3. Переходим в левом меню в раздел **"Датасет"**.
![dataset-lists](/images/datalens-bitrix24/dataset-lists.png)
4. Нажимаем кнопку **"Создать"** в открывшемся слайдере задаем параметры нашего датасета.
![dataset-create.png](/images/datalens-bitrix24/create-dataset.png)
5. Выбираем подключение из которого будет выполняться выборка данных. Выбираем из списка ранее добавленое подключение.
![dataset-lists-add](/images/datalens-bitrix24/dataset-lists-add.png)
![dataset-add](/images/datalens-bitrix24/dataset-add.png)
6. После добавления подключения в датасет, будет отображен список доступных таблицы для выборки данных.
  - **Описание таблиц:**
    
    |Название таблицы|Описание|
    |:-------|-------:|
    |crm_deal|таблица c данными по сделкам|
    |crm_lead|таблица с данными по лидам|
    |crm_company|таблица с данными по компаниям|
    |crm_contact|таблица с данными по контактами|
    |crm_deal_stage_history|таблица с историей по стадиям сделок|
    |crm_lead_status_history|таблица с историей по стадиям лидов|
    |socialnetwork_group|таблица с перечнем групп **"Модуля социальная сеть"**|
    |telephony_call|таблица с данными по звонкам|
    |crm_activity|таблица с активностям сущностей CRM|
    
![dataset-table-list](/images/datalens-bitrix24/dataset-table-list.png)

 - Переходим на вкладку **"Поля"**, на данной вкладке будут отображены все доступные поля из таблицы:
   - Имя поля
   - Источник поля
   - Тип
   - Агрегация
   - Описание поля
    
  - Данные в поля будут загружены автоматически согласно данным вашего Битрикс24, все поля изменяемы есть возможность настроить агрегацию данных прямо в датасете 

7. Для редактирования полей выбрать нужное поле, двойным кликом перейти в режим редактирования. Откроется форма редактирования поля, доступные поля для редактирования:
 - ID поля
 - Источник
 - Поле источника
 - Тип поля **(доступные типы полей)**:
    - Дата
    - Дата и время
    - Дробное число
    - Логический
    - Строка
    - Целое число
 - Агрегация **(список функций)**:
    - Нет (не выполнять агрегацию значений)
    - Количество (сумма значений)
    - Количество уникальные (сумма уникальных значений)
    - Максимум (максимальное значение)
    - Минимум (минимальное значение)
    - Среднее (среднее значение)
![ataset-fields-list](/images/datalens-bitrix24/dataset-fields-list.png)
      
8. Добавление параметров датасета, это переменная датасета или чарта, которая может заменять константные значения в вычисляемых полях.
 - Для добавления нажать кнопку **"Добавить"**, в форме добавления указать следующие параметры:
   - Название переменной (не допускаются значения которые начинаются с "_", зарезервированы значения **"tab, state, mode, focus, grid, tz, from, to."**, длина не более 36 символов)
   - Тип
   - Значение по умолчанию 
![dataset-params](/images/datalens-bitrix24/dataset-params.png)
![dataset-fields-add](/images/datalens-bitrix24/dataset-fields-add.png)
     
9. По завершению настроек датасета нажимаем кнопку "Сохранить".

### 4. Настройка чартов в DataLens
1. Чарт — это визуализация данных из **датасета** в виде таблицы, диаграммы или картограммы, переходим в раздел Чарты.
У нас уже имеются предустановленные чарты которые мы может использовать. Если необходимо создать свой чарт нажимаем кнопку **"Создать"**.
![chart-lists](/images/datalens-bitrix24/chart-lists.png)

2. В форме указываем ранее созданный нами датасет на основе которого хотим построить наш чарт
![chart-add](/images/datalens-bitrix24/chart-add.png)
   
3. Выбираем тип диаграммы для отображения данных, доступные типы диаграмм:
  - Линейная диаграмма
  - Накопительная диаграмма с областями
  - Нормированная диаграмма с областями
  - Столбчатая диаграмма
  - Нормированная столбчатая диаграмма
  - Линейчатая диаграмма
  - Нормированная линейчатая диаграмма
  - Точечная диаграмма
  - Круговая диаграмма 
  - Кольцевая диаграмма 
![chart-settings](/images/datalens-bitrix24/chart-settings.png)
    
4. 