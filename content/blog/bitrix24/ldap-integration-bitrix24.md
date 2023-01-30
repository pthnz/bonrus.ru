---
title: "Настройка интеграции Active Directory c Битрикс24"
date: 2022-10-18T11:17:15+03:00
slug: ""
description: "Описание настройки базовой интеграции Active Directory с Битрикс24"
keywords: [Active-Directory, Bitrix24,Интеграция с Битрикс24,Настройка]
draft: true
tags: [Bitrix24,Active-Directory,Integration]
math: false
toc: true
---

## Настройка интеграции Active Directory c Битрикс24

1. Настройка Active Directory (Windows Server 2012 R2)
2. Настройка доменных служб Active Directory.     
3. Добавление пользователей домена.   
4. Добавление подключения к Active Directory в Битрикс24.
5. Настройка соответствия групп пользователей.
6. Экспорт пользователей в Битрикс24
7. Включение NTLM авторизации в Битрикс24.

---

### Настройка Active Directory (Windows Server 2012 R2)

1. Добавление роли "Доменные службы Active Directory" для сервера.

   - Start -> Server Manager (Пуск -> Диспетчер сервера).
   - Add roles and features -> Next
   - Выбрать Role-based or feature-based Installation (Установка ролей и компонентов)  -> Next
     ![add-role-ad](/images/AD-Bitrix24/srv2012-add-role-ad-01.png)
   - Выбрать сервер, на который устанавливается роль AD и нажать Далее. Select a server from the server pool -> Next
    ![select-ad-server](/images/AD-Bitrix24/)
   - Выбираем роль Active Directory Domain Services (Доменные службы Active Directory), после чего появляется окно с предложением добавить роли и компоненты, необходимые для установки роли AD. Нажимаем кнопку Add Features.
    ![server-roles](/images/AD-Bitrix24/)
     
2. Настройка доменных служб Active Directory.
   - После установки роли, закрыть окно — Close. Теперь необходимо перейти к настройке роли AD.
   - В окне Server Manager нажать пиктограмму флага с уведомлением и нажать Promote this server to a domain controller (Повысить роль этого сервера до уровня контроллера домена) на плашке Post-deploiment Configuration.