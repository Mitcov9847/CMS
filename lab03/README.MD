Лабораторная работа №3
Разработка простой темы WordPress
Цель работы

Научиться создавать собственную тему WordPress, разобраться в её минимальной структуре и принципах работы шаблонов.

Шаг 1. Подготовка среды
В локальной установке WordPress перешёл в папку:
wp-content/themes
Создал директорию для темы:
usm-theme
Включил отладку в wp-config.php для отображения ошибок:
define('WP_DEBUG', true);

Скриншот:


Пояснение:
Это позволяет создавать тему и сразу видеть ошибки в коде, чтобы корректно её настраивать.

Шаг 2. Создание обязательных файлов темы
В папке темы создал файл style.css с метаданными:
/*
Theme Name: USM Theme
Author: Евгений Митков
Description: Простая тема для лабораторной работы №3
Version: 1.0
*/
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
}
Создал файл index.php с базовой HTML-структурой:
<?php get_header(); ?>

<div class="container">
    <main class="content">
        <?php
        $args = array('posts_per_page' => 5);
        $latest_posts = new WP_Query($args);
        if ($latest_posts->have_posts()) :
            while ($latest_posts->have_posts()) : $latest_posts->the_post(); ?>
                <article class="post">
                    <h2><a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></h2>
                    <div><?php the_excerpt(); ?></div>
                </article>
        <?php endwhile; endif; wp_reset_postdata(); ?>
    </main>
    <?php get_sidebar(); ?>
</div>

<?php get_footer(); ?>

Скриншот:


Пояснение:
index.php — основной шаблон темы, здесь выводятся последние 5 постов с помощью стандартного цикла WordPress.

Шаг 3. Общие части шаблонов
header.php
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
footer.php
<footer>
    <p>&copy; <?php echo date('Y'); ?> USM Theme</p>
</footer>
<?php wp_footer(); ?>
</body>
</html>

Пояснение:

get_header() подключает шапку сайта
get_footer() подключает подвал
Общие части используются на всех страницах для единообразия

Скриншот:


Шаг 4. Файл функций (functions.php)
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

Пояснение:

Подключение стилей темы через wp_enqueue_style
Регистрация меню для боковой панели
Шаг 5. Дополнительные шаблоны
single.php
<?php get_header(); ?>
<div class="container">
    <main class="content">
        <?php if(have_posts()) : while(have_posts()) : the_post(); ?>
            <article class="post">
                <h2><?php the_title(); ?></h2>
                <div><?php the_content(); ?></div>
            </article>
            <?php comments_template(); ?>
        <?php endwhile; endif; ?>
    </main>
    <?php get_sidebar(); ?>
</div>
<?php get_footer(); ?>
page.php
<?php get_header(); ?>
<div class="container">
    <main class="content">
        <?php if(have_posts()) : while(have_posts()) : the_post(); ?>
            <article class="page">
                <h2><?php the_title(); ?></h2>
                <div><?php the_content(); ?></div>
            </article>
        <?php endwhile; endif; ?>
    </main>
    <?php get_sidebar(); ?>
</div>
<?php get_footer(); ?>
sidebar.php (только навигация)
<aside class="sidebar">
    <h3>Навигация</h3>
    <ul class="sidebar-menu">
        <li><a href="<?php echo home_url(); ?>">Главная</a></li>
        <li><a href="<?php echo get_permalink(get_page_by_title('О нас')); ?>">О нас</a></li>
        <li><a href="<?php echo get_permalink(get_option('page_for_posts')) ?: home_url(); ?>">Записи</a></li>
    </ul>
</aside>

Пояснение:
Боковая панель показывает только нужные ссылки: Главная → О нас → Записи.

Скриншот:


comments.php
<?php
if ( comments_open() || get_comments_number() ) :
    comments_template();
endif;
archive.php
<?php get_header(); ?>
<div class="container">
    <main class="content">
        <h2>Архив записей</h2>
        <?php if(have_posts()) : while(have_posts()) : the_post(); ?>
            <article>
                <h3><a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></h3>
            </article>
        <?php endwhile; endif; ?>
    </main>
    <?php get_sidebar(); ?>
</div>
<?php get_footer(); ?>
Шаг 6. Стилизация темы

Пример базовых стилей в style.css:

body { font-family: Arial, sans-serif; margin:0; padding:0; }
header, footer { background:#333; color:#fff; padding:15px; text-align:center; }
.container { display:flex; gap:20px; padding:20px; }
.content { flex:3; }
.sidebar { flex:1; background:#f0f0f0; padding:15px; }
.post, .page { margin-bottom:20px; }
.sidebar-menu { list-style:none; padding:0; }
.sidebar-menu li { margin-bottom:10px; }
.sidebar-menu a { text-decoration:none; color:#333; }

Скриншот:


Шаг 7. Скриншот темы
Файл screenshot.png добавлен в папку темы (usm-theme)
Размер: 1200x900 px
Показывает вид главной страницы с боковой панелью
Шаг 8. Активация темы
WordPress → Внешний вид → Темы
Найти тему USM Theme
Нажать Активировать
Проверить работу сайта на главной, страницах, записях

Скриншот:


Контрольные вопросы

1. Какие два файла являются обязательными для любой темы WordPress?

index.php
style.css

2. Как подключаются общие части шаблонов (header, footer, sidebar)?

get_header(), get_footer(), get_sidebar()

3. Чем отличаются index.php, single.php и page.php?

index.php — главный шаблон темы
single.php — отдельная запись (пост)
page.php — страницы сайта

4. Зачем нужен файл functions.php в теме?

Подключает стили и скрипты
Регистрирует меню и виджеты
Расширяет функционал темы без изменения ядра WordPress
