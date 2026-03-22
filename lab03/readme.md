# Лабораторная работа №3: Разработка простой темы WordPress

## Цель работы
Научиться создавать собственную тему WordPress, разобраться в минимальной структуре темы и принципах работы шаблонов.


## Инструкция по запуску
1. Установить WordPress.
2. Скопировать папку темы `usm-theme` в `wp-content/themes`.
3. Активировать тему в разделе **Appearance → Themes (Внешний вид → Темы)**.

## Ход работы

### Шаг 1. Подготовка среды
Перед началом разработки необходимо подготовить рабочую среду:

- Используется локальный сервер XAMPP с Apache и MySQL (MariaDB).
- Проверена работа WordPress.
- В папке `wp-content/themes` создана директория темы: `usm-theme`.


Включён режим отладки WordPress, изменён параметр в `wp-config.php`:

```php
define('WP_DEBUG', true);
```
<img width="1266" height="149" alt="image" src="https://github.com/user-attachments/assets/dacdaff6-1d38-436d-9b39-730740ce414e" />
Это позволяет видеть ошибки и предупреждения для упрощения разработки.

### Шаг 2. Создание обязательных файлов темы

Минимальная тема WordPress должна содержать два файла:
```
1. style.css — содержит метаданные темы и базовые стили.
2. index.php — главный шаблон темы, выводит контент сайта.
```
Структура папки темы после создания:

<img width="200" height="132" alt="image" src="https://github.com/user-attachments/assets/4570c5f1-0529-459b-8a76-36d5651ebedd" />

### Шаг 3. Дополнительные шаблоны

## 1. `style.css`
<img width="350" height="400" alt="image" src="https://github.com/user-attachments/assets/0bb2b2f2-aa4f-40b5-af6b-a5ea3e882815" />
<img width="300" height="400" alt="image" src="https://github.com/user-attachments/assets/73763a76-c444-4b72-9fe0-442ee6d5d0ad" />

---
- Содержит метаданные темы: название, автор, описание, версия.
- Определяет базовые CSS-правила для всех элементов сайта:
  - `body` — шрифт, цвет текста, фон, отступы.
  - `header` и `footer` — стили шапки и подвала.
  - `main`, `.posts-section`, `.posts-container`, `.post-card` — оформление основного контента и карточек записей.
  - `.sidebar-box` — стили боковой панели.
  - `.comments-area` и `.comment-respond` — оформление комментариев и формы их добавления.
- Позволяет задать сетку, тени, отступы и визуальное оформление блоков.
---

## 2. `index.php`
<img width="350" height="400" alt="image" src="https://github.com/user-attachments/assets/5fae3865-9f9a-4ca3-909c-a92cac7a0c05" />

---
- Содержит метаданные темы: название, автор, описание, версия.
- Определяет базовые CSS-правила для всех элементов сайта:
  - `body` — шрифт, цвет текста, фон, отступы.
  - `header` и `footer` — стили шапки и подвала.
  - `main`, `.posts-section`, `.posts-container`, `.post-card` — оформление основного контента и карточек записей.
  - `.sidebar-box` — стили боковой панели.
  - `.comments-area` и `.comment-respond` — оформление комментариев и формы их добавления.
- Позволяет задать сетку, тени, отступы и визуальное оформление блоков.
---

## 3. `header.php`
<img width="600" height="516" alt="image" src="https://github.com/user-attachments/assets/33fe30d7-99ec-4bc9-96a6-886fd8cc5aa0" />

---
- Содержит шапку сайта и подключение всех стилей и скриптов.
- HTML-документ начинается с `<!DOCTYPE html>` и `<html>`.
- `bloginfo('name')` выводит название сайта, `bloginfo('description')` — описание.
- `wp_head()` подключает стили, скрипты и плагины WordPress.
- Начало основного блока сайта обёрнуто в `<main>`.
  
---
## `Файл footer.php`
<img width="600" height="317" alt="image" src="https://github.com/user-attachments/assets/3a77b861-d443-4383-ac3a-2b8fe6cef07d" />

---
- Содержит подвал сайта и завершает структуру страницы.
- Выводит текущий год через `date('Y')`.
- `wp_footer()` подключает скрипты и необходимые элементы перед закрытием страницы.
- Закрывает теги `main`, `footer`, `body` и `html`.
  
---

## Файл функций `functions.php`
<img width="600" height="281" alt="image" src="https://github.com/user-attachments/assets/c81ef7dc-9da7-4ae1-8862-b11321d227a0" />

Пояснение:
Подключает стили темы (style.css).
Регистрирует меню для боковой панели.

### Шаг 4. Дополнительные шаблоны

## `single.php` — страница сайта
<img width="600" height="530" alt="image" src="https://github.com/user-attachments/assets/6d8cf0ee-7cca-4f5c-bdda-247f3b86f67a" />

---
- Боковая панель сайта.
- Содержит блок навигации `<aside>`.
- Список ссылок `<ul>` и `<li>` создаёт пункты меню.
- `home_url()` возвращает URL главной страницы сайта.
- Используется в шаблонах через `get_sidebar()`.

---
  
## `page.php` — страница сайта
<img width="600" height="490" alt="image" src="https://github.com/user-attachments/assets/4bed13c9-0532-4339-a20a-254846094271" />

---
- Шаблон для статических страниц сайта (например, «О нас» или «Контакты»).
- Структура почти идентична `single.php`.
- Использует цикл WordPress для вывода заголовка (`the_title()`) и содержимого страницы (`the_content()`).
- Подключает боковую панель и подвал.
  
---

## `sidebar.php` — боковая панель
<img width="600" height="470" alt="image" src="https://github.com/user-attachments/assets/33579d27-964b-4098-8187-706cc8cee5b2" />

---
- Боковая панель сайта.
- Содержит блок навигации `<aside>`.
- Список ссылок `<ul>` и `<li>` создаёт пункты меню.
- `home_url()` возвращает URL главной страницы сайта.
- Используется в шаблонах через `get_sidebar()`.

  ---
### Шаг 5. Стилизация темы

На данном этапе мы добавляем оформление для всех основных элементов темы WordPress. Файл `style.css` содержит CSS-правила для:

- **Шапки (header)** и **подвала (footer)** сайта;
- Основного контента, включая блоки с последними записями и карточки записей;
- **Боковой панели (sidebar)** с навигацией по сайту;
- **Комментарии (comments)** — список комментариев и форма добавления нового комментария.

Пример кода из style.css:
```
header{
    background:#333;
    color:white;
    text-align:center;
    padding:40px 20px;
}

footer{
    background:#222;
    color:white;
    text-align:center;
    padding:25px;
    margin-top:40px;
}

.posts-container{
    display:grid;
    grid-template-columns:1fr;
    gap:20px;
}

.sidebar-box{
    background:#f7f7f7;
    border:1px solid #ddd;
    border-radius:10px;
    padding:20px;
}
```
### Шаг 6. Скриншот темы
Для корректного отображения темы в административной панели WordPress необходимо добавить изображение-превью темы.
Данный файл используется системой WordPress для отображения предварительного просмотра темы в разделе управления темами.

Файл необходимо разместить непосредственно в директории темы.
Структура папки темы после добавления изображения имеет следующий вид:

<img width="248" height="442" alt="image" src="https://github.com/user-attachments/assets/2ea3b25e-b860-4c4d-921d-9603538afee0" />


### Шаг 7. Активация темы
Перейти в Appearance → Themes.
Найти тему USM Theme.
Нажать Activate.
Открыть главную страницу сайта и проверить отображение темы.

<img width="1407" height="1054" alt="image" src="https://github.com/user-attachments/assets/d6ba38ea-d2f4-42c6-8328-6616ec75a75d" />

### Шаг 8. Навигация, комментарии и вывод записей

На этом этапе описывается вся работа, проделанная по созданию навигации, отображению записей и подключению комментариев на сайте с пользовательской темой `usm-theme`.

#### 8.1 Навигация

Для удобства пользователей была создана боковая панель сайта (sidebar).  
В ней расположены ссылки на ключевые разделы:

- **Главная страница** — ссылка на главную страницу сайта.  
- **Записи блога** — ссылка на страницу с последними публикациями.  

Пункты меню, которые не требуются (например, контакты или страницы сайта), были удалены.  
Боковая панель подключается на всех страницах и записях, обеспечивая одинаковую навигацию на всём сайте.

<img width="389" height="210" alt="image" src="https://github.com/user-attachments/assets/0882fb35-5d55-4153-a125-dfe4099e5078" />

---

#### 8.2 Вывод записей

На главной странице реализован вывод последних публикаций блога:

- Отображаются заголовок и краткое описание каждой записи.  
- Ссылка на запись позволяет перейти на отдельную страницу с полным текстом.  
- Количество отображаемых записей ограничено, чтобы не перегружать страницу.

Данный функционал обеспечивает удобное представление свежих публикаций для посетителей сайта.

<img width="1277" height="757" alt="image" src="https://github.com/user-attachments/assets/85f5e67f-c48c-48bf-99dd-e53cb936ee00" />

---

#### 9.3 Комментарии

Для взаимодействия с пользователями была создана система комментариев:

- Список комментариев отображается под каждой записью.  
- Пользователь может оставить свой комментарий через форму добавления комментария.  
- Проверяется наличие существующих комментариев и разрешение на добавление новых.

Подключение комментариев выполнено на страницах отдельных записей и страницах сайта, что обеспечивает единообразный вывод информации.

<img width="1259" height="856" alt="image" src="https://github.com/user-attachments/assets/7bf81d69-f4c1-45af-ab22-3f272fc216a2" />

---

## Контрольные вопросы
#### 1. Какие два файла обязательны для любой темы?
```
style.css
index.php
```
#### 2. Как подключаются header, footer, sidebar?
```
get_header()
get_footer()
get_sidebar()
```
#### 3. Чем отличаются index.php, single.php, page.php?
```
index.php — главный шаблон для всех страниц.
single.php — шаблон отдельной записи.
page.php — шаблон статической страницы.
```
#### 4. Зачем нужен functions.php?
Подключает стили и скрипты, регистрирует меню и виджеты, расширяет функциональность темы.

### Список использованных источников

1. **WordPress Documentation** — официальная документация по системе управления контентом WordPress.  
   [https://wordpress.org/support/article/](https://wordpress.org/support/article/)

2. **Theme Developer Handbook** — руководство по разработке пользовательских тем WordPress, включая структуру файлов и использование шаблонов.  
   [https://developer.wordpress.org/themes/](https://developer.wordpress.org/themes/)

3. **Template Hierarchy** — описание иерархии шаблонов WordPress, объясняющее работу файлов index.php, single.php, page.php и других шаблонов темы.  
   [https://developer.wordpress.org/themes/basics/template-hierarchy/](https://developer.wordpress.org/themes/basics/template-hierarchy/)

4. **WordPress Codex** — справочник по функциям, структуре тем и возможностям системы управления контентом WordPress.  
   [https://codex.wordpress.org/](https://codex.wordpress.org/)

5. **Introduction to WordPress Themes** — введение в разработку тем WordPress и объяснение основных принципов работы тем.  
   [https://developer.wordpress.org/themes/getting-started/](https://developer.wordpress.org/themes/getting-started/)
## Выводы

Была создана собственная тема WordPress со всеми обязательными файлами, дополнительными шаблонами, боковой панелью и стилями. Тема успешно активирована и отображает записи, страницы и комментарии.

Библиография
WordPress Documentation
Theme Developer Handbook — Руководство по разработке тем
Template Hierarchy — Иерархия шаблонов WordPress
WordPress Codex — Справочник по функциям и структуре тем

