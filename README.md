# LobbyFX Workshop

Каталог фонів і тем для вкладки **Майстерня** в розширенні LobbyFX.
Розширення читає `catalog.json` через безкоштовний CDN jsDelivr:

```
https://cdn.jsdelivr.net/gh/<твій-нік>/lobbyfx-workshop@main/catalog.json
```

## Як додати фон

1. Поклади файл у `backgrounds/` (WEBP/JPG/PNG/GIF/MP4/WEBM, **до 20 МБ** — це ліміт jsDelivr).
2. Поклади прев'ю 384×216 у `thumbs/` (WEBP, ~10–30 КБ). Для відео прев'ю обов'язкове.
3. Додай запис у `catalog.json`:

```json
{
  "id": "unique-id",                      // латиницею, не змінюй після публікації
  "title": { "uk": "Назва", "en": "Name", "ru": "Название" },
  "type": "image",                        // image | video | youtube
  "src": "backgrounds/file.webp",         // шлях у репозиторії, повне посилання або ID відео YouTube
  "thumb": "thumbs/file.webp",
  "tags": ["anime", "neon"]
}
```

4. Закоміть і запуш. jsDelivr кешує файли до 12 годин; щоб оновити одразу, відкрий
   `https://purge.jsdelivr.net/gh/<твій-нік>/lobbyfx-workshop@main/catalog.json`.

## Як додати тему

Тема — це лише CSS і картинки, без JavaScript. Розширення завантажує її, коли користувач натискає «Застосувати», і саме оновлює, коли ти змінюєш `version`.

1. Створи папку `themes/<id>/` з файлом `theme.css` і картинками (SVG/PNG/WEBP, разом до 6 МБ). Приклад — `themes/sakura/`.
2. У `theme.css` кожне правило починається з `& ` — LobbyFX підставить туди область теми. Картинки з папки: `asset(file.svg)`. Шрифти — лише `@import` з fonts.googleapis.com.
3. Додай запис у масив `themes` у `catalog.json`:

```json
{
  "id": "sakura",                       // латиницею, не змінюй після публікації
  "version": 1,                         // збільш, коли змінюєш тему — у користувачів оновиться
  "title": { "uk": "Сакура", "en": "Sakura", "ru": "Сакура" },
  "desc":  { "uk": "Опис", "en": "Description", "ru": "Описание" },
  "colors": ["#2a1422", "#ff9ec2", "#ffe9f1"],   // 3 кольори для картки теми
  "css": "themes/sakura/theme.css",
  "assets": ["blossom.svg", "petals.svg"],       // файли з папки теми
  "playText": ""                                 // текст кнопки пошуку за замовчуванням, напр. "Uwu<3"
}
```

4. Закоміть, потім відкрий `https://purge.jsdelivr.net/gh/whyvvsSEO/lobbyfx-workshop@main/catalog.json` (і для зміненого `theme.css`), щоб не чекати кеш jsDelivr до 12 годин.

### Що можна стилізувати

LobbyFX сам розмічає елементи FACEIT за кольором і розміром:

| Селектор | Що це |
| --- | --- |
| `[data-bc="base"]` | великі темні підкладки сторінки |
| `[data-bc="panel"]` | панелі й картки |
| `[data-bc="slot"]`, `[data-bc="tile"]` | світлі плашки, картки паті |
| `[data-bc="btn"]` / `[data-bc="btn-go"]` | звичайні / помаранчеві кнопки |
| `[data-bc="xp"]` | тонкі смуги прогресу |
| `[data-bc="accent"]`, `[data-bc="lime"]` | помаранчевий / салатовий текст |

Стабільні шматки класів FACEIT: `[class*="LocalNavigationWrapper"]` (верхнє меню), `[class*="PlayButtonWrapper__Container"] button` (кнопка пошуку), `[class*="EloWidget-module"] [class*="ProgressBar__Progress"]` (смуга ELO, `::before` — заповнення, `var(--lfx-prog)` — де воно закінчується), `[class*="styles__CanvasHolder"]` (фон), `[class*="NavigationSidebarHolder"]`, `[class*="AccountSidebarHolder"]` (бокові панелі).

## Правила

- Тільки фони, які ти маєш право поширювати: власні, з дозволу автора або з вільною ліцензією (CC0, Pexels, Unsplash тощо).
- Кадри з аніме, ігор і фільмів без дозволу правовласника сюди не клади.
- Прибери з репозиторію приклади (`example-*`) перед публікацією.

## Підключення в розширенні

Уже підключено: розширення читає `https://cdn.jsdelivr.net/gh/whyvvsSEO/lobbyfx-workshop@main/catalog.json`.
