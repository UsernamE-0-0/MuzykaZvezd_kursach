# Музыка звёзд — курсач

Веб-приложение для выбора области неба и генерации музыки по данным звёзд Gaia.

## Возможности

- Интерактивная карта Aladin Lite с обзором DSS.
- Генерация музыки в стилях ambient, classical, spacewave и experimental.
- Регистрация, профиль и история генераций в PostgreSQL.
- Локальный чат поддержки через WebSocket.

## Локальный запуск

Нужны Node.js с npm и PostgreSQL. Создайте базу `starmusic`.

Скопируйте `.env.example` в `.env`, а `backend/.env.example` в `backend/.env`.
Укажите свои `DATABASE_URL` и `JWT_SECRET`. Файлы `.env` не должны попадать в Git.

Терминал 1, из корня проекта:

```powershell
cd backend
npm ci
npx prisma generate
npx prisma migrate deploy
npm run dev
```

Терминал 2, из корня проекта:

```powershell
npm ci
npm run server
```

Терминал 3, из корня проекта:

```powershell
npm run dev
```

Откройте http://localhost:5173. Основной API работает на порту 4000, прокси Gaia и чат — на порту 3000.
Ответы оператора чата вводятся в терминале `npm run server` и отправляются всем подключённым пользователям.

## Карта и сторонний код

Aladin Lite v2 и jQuery находятся в `public/vendor/aladin-v2` и загружаются локально.
Изображения DSS загружаются с зеркала NASA/IPAC IRSA; данные звёзд — из Gaia через `server.js`.
Для этих данных требуется интернет.

Aladin Lite распространяется по GPL-3.0. Лицензия, исходный архив и сведения о локальных изменениях находятся в `public/vendor/aladin-v2`.
Уведомление о лицензии jQuery сохранено в начале его файла.

## Сборка

```powershell
npm run build
```

Проект учебный. Перед размещением в интернете необходима отдельная проверка прав доступа к генерациям, прокси Gaia и авторизации чата.