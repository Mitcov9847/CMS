# Лабораторная работа №3: Разработка простой темы WordPress

## Цель работы
Научиться создавать собственную тему WordPress, разобраться в минимальной структуре темы и принципах работы шаблонов.

---

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

**Скриншот VS Code:**  
![Подготовка среды](./screenshots/step1.png)

Включён режим отладки WordPress, изменён параметр в `wp-config.php`:

```php
define('WP_DEBUG', true);

Это позволяет видеть ошибки и предупреждения для упрощения разработки.

Шаг 2. Создание обязательных файлов темы

Минимальная тема WordPress должна содержать два файла:

style.css — содержит метаданные темы и базовые стили.
index.php — главный шаблон темы, выводит контент сайта.

Структура папки темы после создания:

usm-theme/
    style.css
    index.php
Файл style.css

Пример содержимого:

/*
Theme Name: USM Theme
Author: Student
Description: Простая тема WordPress для лабораторной работы
Version: 1.0
*/

body {
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
}

Скриншот VS Code:


Файл index.php

Пример содержимого:

<?php get_header(); ?>

<section class="posts-section">
    <h2>Последние записи</h2>

    <?php
    $count = 0;
    if (have_posts()) :
        while (have_posts()) : the_post();
            if ($count == 5) break;
    ?>
        <div class="post-card">
            <h3><a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></h3>
            <p><?php the_excerpt(); ?></p>
        </div>
    <?php
            $count++;
        endwhile;
    endif;
    ?>
</section>

<?php get_footer(); ?>

Скриншот VS Code:


Пояснение:

get_header() и get_footer() подключают шапку и подвал.
WordPress Loop (have_posts() / the_post()) выводит последние записи.
$count ограничивает количество выводимых постов.
Шаг 3. Общие части шаблонов
Файл header.php
<!DOCTYPE html>
<html <?php language_attributes(); ?>>
<head>
    <meta charset="<?php bloginfo('charset'); ?>">
    <title><?php bloginfo('name'); ?></title>
    <?php wp_head(); ?>
</head>
<body>
<header>
    <h1><?php bloginfo('name'); ?></h1>
    <p><?php bloginfo('description'); ?></p>
</header>
<main>

Скриншот VS Code:


Файл footer.php
</main>
<footer>
    <p>© <?php echo date('Y'); ?> USM Theme</p>
</footer>
<?php wp_footer(); ?>
</body>
</html>

Скриншот VS Code:


Шаг 4. Файл функций functions.php
<?php
function usm_theme_styles() {
    wp_enqueue_style('usm-style', get_stylesheet_uri());
}
add_action('wp_enqueue_scripts', 'usm_theme_styles');

function usm_theme_menus() {
    register_nav_menus(array(
        'sidebar-menu' => 'Меню боковой панели'
    ));
}
add_action('after_setup_theme', 'usm_theme_menus');

Скриншот VS Code:


Пояснение:

Подключает стили темы (style.css).
Регистрирует меню для боковой панели.
Шаг 5. Дополнительные шаблоны
single.php — отдельная запись
<?php get_header(); ?>
<section class="content-page">
    <div class="content-main">
        <?php if (have_posts()) : while (have_posts()) : the_post(); ?>
            <article>
                <h3><?php the_title(); ?></h3>
                <div><?php the_content(); ?></div>
            </article>
            <?php comments_template(); ?>
        <?php endwhile; endif; ?>
    </div>
    <div class="content-side"><?php get_sidebar(); ?></div>
</section>
<?php get_footer(); ?>
page.php — страница сайта
<?php get_header(); ?>
<section class="content-page">
    <div class="content-main">
        <?php if (have_posts()) : while (have_posts()) : the_post(); ?>
            <article>
                <h3><?php the_title(); ?></h3>
                <div><?php the_content(); ?></div>
            </article>
        <?php endwhile; endif; ?>
    </div>
    <div class="content-side"><?php get_sidebar(); ?></div>
</section>
<?php get_footer(); ?>
sidebar.php — боковая панель
<aside class="sidebar-box">
    <h3>Навигация</h3>
    <ul>
        <li><a href="<?php echo home_url(); ?>">Главная</a></li>
        <li><a href="<?php echo home_url('/?page_id=2'); ?>">Страницы сайта</a></li>
        <li><a href="<?php echo home_url(); ?>">Записи блога</a></li>
    </ul>
</aside>
Шаг 6. Стилизация темы

Файл style.css содержит стили для:

шапки и подвала,
основного контента и карточек записей,
боковой панели,
комментариев.

Скриншот VS Code:


Шаг 7. Скриншот темы

Добавлен файл screenshot.png в папку темы для отображения превью в WordPress.

Структура папки темы:

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
Шаг 8. Активация темы
Перейти в Appearance → Themes.
Найти тему USM Theme.
Нажать Activate.
Открыть главную страницу сайта и проверить отображение темы.
Контрольные вопросы

1. Какие два файла обязательны для любой темы?

style.css
index.php

2. Как подключаются header, footer, sidebar?

get_header()
get_footer()
get_sidebar()

3. Чем отличаются index.php, single.php, page.php?

index.php — главный шаблон для всех страниц.
single.php — шаблон отдельной записи.
page.php — шаблон статической страницы.

4. Зачем нужен functions.php?

Подключает стили и скрипты, регистрирует меню и виджеты, расширяет функциональность темы.
Выводы

Была создана собственная тема WordPress со всеми обязательными файлами, дополнительными шаблонами, боковой панелью и стилями. Тема успешно активирована и отображает записи, страницы и комментарии.

Библиография
WordPress Documentation
Theme Developer Handbook — Руководство по разработке тем
Template Hierarchy — Иерархия шаблонов WordPress
WordPress Codex — Справочник по функциям и структуре тем

---
