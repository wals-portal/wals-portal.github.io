# Свой WALS-портал для Media Station X (MSX)

Это твой собственный минимальный аналог W.A.L.S — экран запуска веб-приложений
для MSX на LG webOS. Каждая плитка — это отдельный веб-сайт, который открывается
действием `link:` без установки нативного приложения.

## Структура

```
wals-portal/
├── start.json          # точка входа (Start Parameter)
└── data/
    ├── menu.json        # боковое меню (категории)
    ├── apps.json         # плитки: избранное / общие приложения
    ├── movies.json        # плитки: кино и ТВ
    ├── music.json          # плитки: музыка
    └── tools.json           # плитки: твой хомлаб (qBittorrent, HA, MikroTik и т.д.)
```

## Как это работает

- `start.json` указывает MSX, какое меню грузить при старте (`menu:URL`).
- `menu.json` — это список пунктов слева (категории), каждый пункт грузит свой
  JSON с плитками через `data`.
- Каждый файл с плитками (`apps.json` и т.д.) — это `Content Root Object` с
  `template` (общий стиль плитки) и `items` (сами плитки).
- Действие `link:{URL}` открывает сайт во встроенном вьюпорте MSX, а
  `link:window:{URL}` — в отдельном окне/внешнем браузере (полезно, если сайт
  плохо работает во встроенном вьюпорте, например YouTube).

## Установка

1. Замени во всех файлах `USERNAME.github.io/wals-portal` на свой реальный адрес
   (например `voipoddsns.github.io/wals-portal`, если положишь в подпапку
   существующего репозитория, или заведи отдельный репозиторий `wals-portal`).
2. Замени плейсхолдеры (URL, IP локальных сервисов, названия приложений) на
   свои реальные адреса — сейчас там просто примеры для наглядности.
3. Залей папку в GitHub Pages (публичный репозиторий → Settings → Pages →
   ветка с файлами).
4. Проверь, что `https://ТВОЙ_АДРЕС/wals-portal/start.json` открывается и
   отдаёт валидный JSON.
5. На телевизоре: Media Station X → Settings → Start Parameter → Setup →
   ввести адрес **без `https://`**, например:
   `ТВОЙ_АДРЕС/wals-portal/start.json`
   (или, как в оригинальном WALS, можно указать просто `menu.json` напрямую,
   если хочешь пропустить start.json).

## Полезное

- Список доступных иконок: https://msx.benzac.de/wiki/index.php?title=Icons
- Список цветов (`color`): https://msx.benzac.de/wiki/index.php?title=Colors
- Все действия (`link:`, `video:`, `menu:` и т.д.):
  https://msx.benzac.de/wiki/index.php?title=Actions
- Полный справочник по JSON-структурам:
  https://msx.benzac.de/wiki/index.php?title=Welcome

## Как добавить новую плитку

В любой из файлов `data/*.json` в массив `items` добавь объект:

```json
{
    "id": "unique_id",
    "icon": "имя_иконки",
    "label": "Название",
    "action": "link:window:https://example.com"
}
```

`layout`, `color`, `iconSize` брать не нужно — они уже заданы в `template` и
применяются ко всем плиткам файла автоматически.
