# JavaScript SDK Maticon Office DocSpace

[RU](README.md) | [EN](README.en.md)

## Основные понятия

JavaScript SDK Maticon Office DocSpace позволяет разработчикам использовать все возможности DocSpace через *api.js*. Maticon Office DocSpace можно встроить в собственное веб-приложение, чтобы пользователи могли создавать и отправлять документы непосредственно с вашего сайта. Например, для интеграции Maticon Office DocSpace в React-проекты можно использовать [React-компонент DocSpace](https://api.maticonoffice.ru/docspace/javascript-sdk/get-started/react-component/).

Для работы с JavaScript SDK DocSpace не требуется большой опыт разработки на JavaScript: базовая интеграция настраивается несколькими строками кода.

Чтобы подключить DocSpace к сайту во фрейме, выполните следующие действия.

## Шаг 1. Укажите URL DocSpace

Для корректной работы JavaScript SDK страницу необходимо запускать с сервера. Прямое открытие HTML-файла не поддерживается. Убедитесь, что страница доступна через серверное окружение.

Добавьте URL корневого каталога своего сервера в раздел **Инструменты разработчика** DocSpace:

1. Откройте настройки DocSpace.
2. Перейдите в раздел **Инструменты разработчика**.
3. На вкладке **JavaScript SDK** добавьте URL корневого каталога сервера в поле **Введите адрес DocSpace для встраивания**.

## Шаг 2. Создайте HTML-файл

Создайте целевой HTML-файл с элементом-заполнителем *div*, в который будет передана информация о параметрах DocSpace:

```html
<!DOCTYPE html>
<html lang="ru">
  <head>
    <meta charset="UTF-8">
    <title>DocSpace JavaScript SDK</title>
    <script src="{PORTAL_SRC}/static/scripts/sdk/2.0.0/api.js"></script>
  </head>
  <body>
    <div id="ds-frame"></div>
  </body>
</html>
```

JavaScript-файл API обычно доступен в следующем каталоге DocSpace:

`{PORTAL_SRC}/static/scripts/sdk/2.0.0/api.js`

Здесь **{PORTAL_SRC}** - адрес сервера, на котором установлен Maticon Office DocSpace.

## Шаг 3. Получите базовый класс

После подключения JavaScript-файла API к странице получите базовый класс, предоставляющий основную функциональность *api.js*:

| Класс | Описание |
|-------|----------|
| DocSpace.SDK | Определяет диспетчер документов DocSpace и позволяет выполнять операции с комнатами, папками и документами на портале DocSpace. |

## Шаг 4. Выполните авторизацию

Для аутентификации пользователей *api.js* использует активные сеансы приложения DocSpace. Если пользователь уже вошёл на портал DocSpace, к которому подключается SDK, *api.js* распознает и использует этот активный сеанс.

Если пользователь не аутентифицирован, при первом обращении к DocSpace откроется страница входа. Аутентификацию также можно выполнить через [методы SDK](https://api.maticonoffice.ru/docspace/javascript-sdk/usage-sdk/methods/#login).

## Шаг 5. Инициализируйте SDK

> При работе через HTTPS необходимо установить параметр **"SameSite": "none"** в *appsettings.json*, чтобы браузер не блокировал cookie в междоменных запросах.

Инициализируйте фрейм DocSpace методом [initFrame](https://api.maticonoffice.ru/docspace/javascript-sdk/usage-sdk/methods/#initframe), передав ему конфигурацию SDK:

```ts
const docSpace = DocSpace.SDK.initFrame({
  frameId: "frameId",
  showMenu: true,
});
```

Для инициализации DocSpace можно использовать и другие доступные [методы](https://api.maticonoffice.ru/docspace/javascript-sdk/usage-sdk/methods/).

Полный список [параметров конфигурации](https://api.maticonoffice.ru/docspace/javascript-sdk/usage-sdk/config/) приведён в документации.

## Шаг 6. Используйте экземпляр SDK

После инициализации текущий экземпляр SDK доступен по его [frameId](https://api.maticonoffice.ru/docspace/javascript-sdk/usage-sdk/config/#frameid). Список текущих экземпляров SDK находится в массиве *DocSpace.SDK.frames*. Чтобы получить конкретный экземпляр SDK, используйте:

```ts
DocSpace.SDK.frames[frameId]
```
