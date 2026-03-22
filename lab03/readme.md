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
style.css — содержит метаданные темы и базовые стили.
index.php — главный шаблон темы, выводит контент сайта.

Структура папки темы после создания:
```
usm-theme/
    archive.php
    comments.php
    footer.php
    functions.php
    header.php
    index.php
    page.php
    sidebar.php
    single.php
    style.css
    screenshot.png
```
<img width="350" height="400" alt="image" src="https://github.com/user-attachments/assets/71fe724b-cc16-4484-a372-bcf344fb5fc6" />

#### Файл style.css
<img width="350" height="400" alt="image" src="https://github.com/user-attachments/assets/0bb2b2f2-aa4f-40b5-af6b-a5ea3e882815" />

#### Файл index.php
<img width="350" height="400" alt="image" src="https://github.com/user-attachments/assets/5fae3865-9f9a-4ca3-909c-a92cac7a0c05" />


#### Пояснение:
get_header() и get_footer() подключают шапку и подвал.
WordPress Loop (have_posts() / the_post()) выводит последние записи.
$count ограничивает количество выводимых постов.

### Шаг 3. Общие части шаблонов
#### Файл header.php
<img width="600" height="516" alt="image" src="https://github.com/user-attachments/assets/33fe30d7-99ec-4bc9-96a6-886fd8cc5aa0" />

#### Файл footer.php
<img width="600" height="317" alt="image" src="https://github.com/user-attachments/assets/3a77b861-d443-4383-ac3a-2b8fe6cef07d" />

### Шаг 4. Файл функций functions.php
<img width="600" height="281" alt="image" src="https://github.com/user-attachments/assets/c81ef7dc-9da7-4ae1-8862-b11321d227a0" />
#### Пояснение:
Подключает стили темы (style.css).
Регистрирует меню для боковой панели.

### Шаг 5. Дополнительные шаблоны

#### .php — страница сайта
<img width="600" height="530" alt="image" src="https://github.com/user-attachments/assets/6d8cf0ee-7cca-4f5c-bdda-247f3b86f67a" />

#### page.php — страница сайта
<img width="600" height="490" alt="image" src="https://github.com/user-attachments/assets/4bed13c9-0532-4339-a20a-254846094271" />

#### sidebar.php — боковая панель
<img width="600" height="470" alt="image" src="https://github.com/user-attachments/assets/33579d27-964b-4098-8187-706cc8cee5b2" />

### Шаг 6. Стилизация темы

Файл style.css содержит стили для:
шапки и подвала,
основного контента и карточек записей,
боковой панели,
комментариев.


### Шаг 7. Скриншот темы

Добавлен файл screenshot.png в папку темы для отображения превью в WordPress.


### Шаг 8. Активация темы
Перейти в Appearance → Themes.
Найти тему USM Theme.
Нажать Activate.
Открыть главную страницу сайта и проверить отображение темы.

## Контрольные вопросы
###### 1. Какие два файла обязательны для любой темы?
```
style.css
index.php
```
######  2. Как подключаются header, footer, sidebar?
```
get_header()
get_footer()
get_sidebar()
```
###### 3. Чем отличаются index.php, single.php, page.php?
```
index.php — главный шаблон для всех страниц.
single.php — шаблон отдельной записи.
page.php — шаблон статической страницы.
```
###### 4. Зачем нужен functions.php?

Подключает стили и скрипты, регистрирует меню и виджеты, расширяет функциональность темы.

## Выводы

Была создана собственная тема WordPress со всеми обязательными файлами, дополнительными шаблонами, боковой панелью и стилями. Тема успешно активирована и отображает записи, страницы и комментарии.

Библиография
WordPress Documentation
Theme Developer Handbook — Руководство по разработке тем
Template Hierarchy — Иерархия шаблонов WordPress
WordPress Codex — Справочник по функциям и структуре тем

---
