---
title: "Отправка уведомления о новом лиде в telegram"
date: 2024-08-12T16:16:10+03:00
slug: "telegram-лид"
description: "Настройка отправка уведомления о лиде в telegram"
keywords: [Bitrix24,Telegram,Интеграция с лидам, CRM]
draft: false
tags: [Bitrix24,Telegram, Integration,CRM]
toc: false
---

#### Создадим telegram бота

1. Войти в telegram, найти аккаунт ```@BotFather```
2. Отправить команду ```/newbot```
3. Указать название бота ```пример:NotificationB24BOT```
4. После успешного создания аккаунт ```@BotFather``` выдаст токен
```
731463547062:AAE9F6UczXP_UpMJj4t6DZmajrSzJ-vfCbE //Пример
```
5. Переходим в Битрикс24, и добавить в профиль сотрудника поле для хранения значения ChatID для отправки сообщений в telegram

![create-user-fields](/images/telegram-notification/create-string-userfield.png)

![create-user-fields](/images/telegram-notification/create-userfield.png)

6. В поле ChatID сотруднику необходимо указать свой ChatID (можно получить с помощью telegram бота ```@chatIDrobot```)

7. Добавляем робота для получения ChatID из профиля пользователя для отправки сообщения о новом лиде. Перейти в раздел со списком лидов выбрать "Роботы" 

![lead-robots.png](/images/telegram-notification/lead-robots.png)

8. Кликнуть на "+" и в поле поиска указать название робота "Получить информацию о сотруднике"

![lead-robots-chatid.png](/images/telegram-notification/lead-robots-chatid.png)
   
9. В поле выбора сотрудника настроек робота, указываем "Ответственный"

![lead-robots-responsible.png](/images/telegram-notification/lead-robots-responsible.png)
   
10. Добавляем робота "Исходящий вебхук", в поле "Хендлер" указываем следующий URL
```phpregexp
https://api.telegram.org/bot{bot_token}/sendMessage?chat_id={chat_id}&text={text}&parseMode=html
```

**Описание:**

bot_token - токен который выдан ```@BotFather```

chat_id - ChatID который будет подставлен из профиля пользователя

text - текст сообщения для отправки

11. Для удобства текст отправляемого сообщения добавить в глобальную переменную.

![lead-robots-var.png](/images/telegram-notification/lead-robots-var.png)

![lead-robots-var-add.png](/images/telegram-notification/lead-robots-var-add.png)

![lead-robots-var-add(example).png](/images/telegram-notification/lead-robots-var-add(example).png)

12. Перед роботом "Исходящий вебхук", добавить робота "Изменить переменную" для формирования сообщения которое мы отправим в уведомление.

![lead-robots-var-change.png](/images/telegram-notification/lead-robots-var-change.png)

13. В роботе выбираем переменную для хранения которую создали в п.11 и заполняем текст

**Пример:**
```phpregexp
Создан новый лид №{{ID}}%0AСсылка для просмотра лида: https:/*.bitrix24.ru{{Ссылка на элемент}}
```

**Описание:**

%0A - символ переноса строки

https://*.bitrix24.ru - адрес вашего портала Битрикс24

{{ID}} - ID элемента (в текущем контексте ID лида)

{{Ссылка на элемент}} - ссылка на элемент

![lead-robots-vars-message.png](/images/telegram-notification/lead-robots-vars-message.png)

**Итог:**
После добавления лида в ручном или автоматическом режиме, получаем уведомление в Telegram.

![lead-telegram-notification.png](/images/telegram-notification/lead-telegram-notification.png)


---
**Ограничения:**

1. Для предоставления возможности отправки сообщения боту, сотруднику необходимо открыть чат с ботом в Telegram и нажать кнопку "Начать".