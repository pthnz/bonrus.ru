---
title: "Настройка smtp отправителя в Битрикс24 через почтовый сервис Яндекс"
date: 2024-08-11T00:00:00+03:00
slug: "settings-smtp"
description: "Настройка почты в Битрикс24 (коробка)"
keywords: [Bitrix24,BitrixVM,Настройка smtp в Битрикс24, Битрикс24 настройка почты]
tags: [Bitrix24,BitrixVM]
draft: false
math: false
toc: true
---

#### Возможные варианты отправки писем из Битрикс24/БУС
- через локальный sendmail или postfix.
- через внешний SMTP-сервер без авторизации.
- через внешний сервер с авторизацией путем замены функции отправки почты.

### 1. Включение smtp-сервера

Для включения необходимо добавить директиву в файл /bitrix/.settings.php
```phpregexp
 'smtp' =>
	array (
		'value' =>
		array(
			'enabled' => true,
			'debug' => true, 
			'log_file' => '/var/mailer.log', 
		),
	),
```

**Описание параметров:**

'enable' - Включить smtp;

'debug' - Включение отладки (отображает ошибки, которые могут возникнуть при отправке сообщений);

'log_file' - Путь к файлу лога 

Сохраняем файлы

**Рекомендации:**

 >Правки в файле /bitrix/.settings.php правки вносить с повышенной внимательностью, ошибки могут привести к неработоспособности системы.

### 2. Добавление почтового отправителя через административную панель

Перейти в административную панель {адрес_сайта/портала}/bitrix, открыть раздел "Настройки - Настройка продукта - Почтовые и СМС события - Настройка SMTP"

Нажать на кнопку "Добавить SMTP-отправителя", откроется форма добавления.

![smtp-sender](/images/smtp-bitrix24/add-smtp-sender.png)

Параметры:
 - E-mail
 - Имя отправителя
 - Для всех пользователей (при установке чек-бокса все пользователи портала смогут использовать данного отправителя).
 - Логин
 - Сервер
 - Порт
 - Пароль

Пример:
```phpregexp
 - E-mail: admin@mail.ru
 - Имя отправителя: Тестовый отправитель
 - Для всех пользователей (при установке чек-бокса все пользователи портала смогут использовать данного отправителя).
 - Логин: admin@mail.ru 
 - Сервер: smtp.yandex.ru
 - Порт: 465/587
 - Пароль: admin@mail.ru
```

В почтовом сервисе необходимо включить доступ к ящику через smtp.

![enable-smtp-email-service.png](/images/smtp-bitrix24/enable-smtp-email-service.png)

Для пароля используется пароль приложений, в Яндекс Почта (включение настройки может отличатся в других почтовых сервисах).

Сохранить настройку, после smtp отправитель будет доступен из публичного раздела Битрикс24.

### 3. Настройка почтового отправителя в BitrixVM
Для настройки авторизоваться на сервере через ssh

3.1. Перейти в директорию /root

3.2. Запустить menu.sh скрипт меню BitrixVM (./menu.sh)

3.3. Перейти в раздел меню 6. Configure pool sites > 4. Change e-mail settings on site

3.4. Указать имя сервера (default по умолчанию)

3.5. Указать адрес smtp сервера

3.6. Указать порт 

3.7. Хотим ли использовать smtp аутентификацию (Y)

3.8. Указать логин

3.9. Указать метод smtp аутентификации (указываем auto)

3.10. Использовать TLS подключение (указываем Y)

После завершения обновления файла конфигурации.

Перейти в главное меню в пункт 6. и проверить указанные данные, так же можно выполнить проверку в файле ```/home/bitrix/.msmtprc.```

>Больше информации в официальной документации Битрикс https://dev.1c-bitrix.ru/learning/course/index.php?COURSE_ID=43&LESSON_ID=23612