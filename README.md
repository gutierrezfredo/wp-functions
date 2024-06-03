# Useful WordPress Functions

This is a list of useful WordPress functions that I often reference to enhance or clean up my sites. Please be careful and make backups.

Author: https://github.com/taniarascia

- [Hide WordPress Update Nag to All But Admins](#hide-wordpress-update-nag-to-all-but-admins)
- [Utilize Proper WordPress Titles](#utilize-proper-wordpress-titles)
- [Create Custom WordPress Dashboard Widget](#create-custom-wordpress-dashboard-widget)
- [Remove All Dashboard Widgets](#remove-all-dashboard-widgets)
- [Include Navigation Menus](#include-navigation-menus)
- [Insert Custom Login Logo](#insert-custom-login-logo)
- [Modify Admin Footer Text](#modify-admin-footer-text)
- [Enqueue Styles and Scripts](#enqueue-styles-and-scripts)
- [Enqueue Google Fonts](#enqueue-google-fonts)
- [Modify Excerpt Length](#modify-excerpt-length)
- [Change Read More Link](#change-read-more-link)
- [Change More Excerpt](#change-more-excerpt)
- [Disable Emoji Mess](#disable-emoji-mess)
- [Remove Comments](#remove-comments)
- [Change Media Gallery URL](#change-media-gallery-url)
- [Create Custom Thumbnail Size](#create-custom-thumbnail-size)
- [Add Categories for Attachments](#add-categories-for-attachments)
- [Add Tags for Attachments](#add-tags-for-attachments)
- [Add Custom Excerpt to Pages](#add-custom-excerpt-to-pages)
- [Create a Global String](#create-a-global-string)
- [Support Featured Images](#support-featured-images)
- [Support Search Form](#support-search-form)
- [Excluding pages from search](#excluding-pages-from-search)
- [Disable XMLRPC](#disable-xmlrpcphp)
- [Escape HTML in Posts](#escape-html-in-posts)
- [Create Custom Global Settings](#create-custom-global-settings)
- [Remove WordPress Admin Bar](#remove-wordpress-admin-bar)
- [Add Open Graph Meta Tags](#add-open-graph-meta-tags)
- [Add Custom Post Type](#add-custom-post-type)
- [Implement Preconnect to Google Fonts in Themes](#implement-preconnect-to-google-fonts-in-themes)
- [Add Thumbnail Column to Post Listing](#add-thumbnail-column-to-post-listing)
- [Add Lead Class to First Paragraph](#add-lead-class-to-first-paragraph)
- [Exclude Custom Post Type from Search](#exclude-custom-post-type-from-search)
- [Remove Query String from Static Resources](#remove-query-string-from-static-resources)
- [Disable Website Field From Comment Form](#disable-website-field-from-comment-form)
- [Modify jQuery](#modify-jquery)
- [Disable JSON Rest API](#disable-json-rest-api)
- [Switch Post Type](#switch-post-type)
- [PHP Logger](#php-logger)
- [Always Show Second Bar in TinyMCE](#always-show-second-bar-in-tinymce)
- [Remove Admin Menu Items Depending on User Role](#remove-admin-menu-items-depending-on-user-role)
- [Remove Admin Menu Items Depending on Email Address (Domain)](#remove-admin-menu-items-depending-on-email-address-domain)
- [Reorder Admin Menu Items](#reorder-admin-menu-items)
- [Exclude a Category From WordPress Loops](#exclude-a-category-from-wordpress-loops)
- [Disable the message "JQMIGRATE: Migrate is installed, version 1.4.1"](#user-content-disable-the-message---jqmigrate-migrate-is-installed-version-141)
- [Load heavy 3rd-party scripts later for better performance](#load-heavy-3rd-party-scripts-later-for-better-performance)
- [Adds not-home class to body](#adds-not-home-class-to-body)
- [Use Relevanssi search instead of the default](#use-relevanssi-search-instead-of-the-default)
- [Solves HTTP ERROR when uploading media](#solves-http-error-when-uploading-media)
- [Hides empty categories in products category widget](#hides-empty-categories-in-products-category-widget)
- [Adds post category to the body-class](#adds-post-category-to-the-body-class)
- [Changes the text in Thank you page after checkout on Woocommerce](#changes-the-text-in-Thank-you-page-after-checkout-on-woocommerce)
- [Points the event link to the event website URL in The Events Calendar plugin](#points-the-event-link-to-the-event-website-URL-in-The-Events-Calendar-plugin)
- [Activates Header extra widget area](#activates-header-extra-widget-area-in-enfold)
- [Disables portfolio items on Enfold](#disables-portfolio-items-in-enfold)
- [Adds custom post type to avia builder in Enfold](#Adds-custom-post-type-to-avia-builder-in-enfold)
- [Activates Advanced Layout Builder on Custom Post types in Enfold](#activates-advanced-layout-builder-on-custom-post-types-in-enfold)
- [Hides web field from comment form](#hides-web-field-from-comment-form)
- [Fixes buggy view in events tribe plugin list admin table](#fixes-buggy-view-in-events-tribe-plugin-list-admin-table)
- [Removes items from WP admin toolbar](#removes-items-from-WP-admin-toolbar)

## Hide WordPress Update Nag to All But Admins

```php
/**
 * Hide WordPress update nag to all but admins
 */
 
function hide_update_notice_to_all_but_admin() {
    if ( !current_user_can( 'update_core' ) ) {
        remove_action( 'admin_notices', 'update_nag', 3 );
    }
}
add_action( 'admin_head', 'hide_update_notice_to_all_but_admin', 1 );
```

## Utilize Proper WordPress Titles

Make sure to remove the `<title>` tag from your header.

```php
/**
 * Utilize proper WordPress titles
 */

add_theme_support( 'title-tag' );
```

## Create Custom WordPress Dashboard Widget

```php
/**
 * Create custom WordPress dashboard widget
 */
 
function dashboard_widget_function() {
    echo '
        <h2>Custom Dashboard Widget</h2>
        <p>Custom content here</p>
    ';
}

function add_dashboard_widgets() {
    wp_add_dashboard_widget( 'custom_dashboard_widget', 'Custom Dashoard Widget', 'dashboard_widget_function' );
}
add_action( 'wp_dashboard_setup', 'add_dashboard_widgets' );
```

## Remove All Dashboard Widgets

```php
/**
 * Remove all dashboard widgets
 */
 
function remove_dashboard_widgets() {
    global $wp_meta_boxes;
    
    unset( $wp_meta_boxes['dashboard']['side']['core']['dashboard_quick_press'] );
    unset( $wp_meta_boxes['dashboard']['normal']['core']['dashboard_incoming_links'] );
    unset( $wp_meta_boxes['dashboard']['normal']['core']['dashboard_right_now'] );
    unset( $wp_meta_boxes['dashboard']['normal']['core']['dashboard_plugins'] );
    unset( $wp_meta_boxes['dashboard']['normal']['core']['dashboard_recent_drafts'] );
    unset( $wp_meta_boxes['dashboard']['normal']['core']['dashboard_recent_comments'] );
    unset( $wp_meta_boxes['dashboard']['side']['core']['dashboard_primary'] );
    unset( $wp_meta_boxes['dashboard']['side']['core']['dashboard_secondary'] );

    remove_meta_box( 'dashboard_activity', 'dashboard', 'normal' );
}
add_action( 'wp_dashboard_setup', 'remove_dashboard_widgets' );
```

## Include Navigation Menus

```php
/** 
 * Include navigation menus
 */

function register_my_menu() {
    register_nav_menu( 'nav-menu', __( 'Navigation Menu' ) );
}
add_action( 'init', 'register_my_menu' );
```

Insert this where you want it to appear, and save the menu in **Appearance -> Menus**.

```php
wp_nav_menu( array( 'theme_location' => 'nav-menu' ) );
```

Here's the code for multiple menus:

```php
function register_my_menus() {
    register_nav_menus(
        array(
            'new-menu' => __( 'New Menu' ),
            'another-menu' => __( 'Another Menu' ),
            'an-extra-menu' => __( 'An Extra Menu' ),
        )
    );
}
add_action( 'init', 'register_my_menus' );
```

## Insert Custom Login Logo

```php
/**
 * Insert custom login logo
 */
 
function custom_login_logo() {
    echo '
        <style>
            .login h1 a { 
                background-image: url(image.jpg) !important; 
                background-size: 234px 67px; 
                width:234px; 
                height:67px; 
                display:block; 
            }
        </style>
    ';
}
add_action( 'login_head', 'custom_login_logo' );
```

## Modify Admin Footer Text

```php
/**
 * Modify admin footer text
 */
 
function modify_footer() {
    echo 'Created by <a href="mailto:you@example.com">you</a>.';
}
add_filter( 'admin_footer_text', 'modify_footer' );
```

## Enqueue Styles and Scripts

```php
/**
 * Enqueue styles and scripts
 */
 
function custom_scripts() {
    wp_enqueue_style( 'bootstrap', get_template_directory_uri() . '/css/bootstrap.min.css', array(), '3.3.6' );
    wp_enqueue_style( 'style', get_template_directory_uri() . '/css/style.css' );
    wp_enqueue_script( 'bootstrap', get_template_directory_uri() . '/js/bootstrap.min.js', array('jquery'), '3.3.6', true );
    wp_enqueue_script( 'script', get_template_directory_uri() . '/js/script.js' );
}
add_action( 'wp_enqueue_scripts', 'custom_scripts' );
```

## Enqueue Google Fonts

```php
/**
 * Enqueue Google Fonts
 */
 
function google_fonts() {
    wp_register_style( 'OpenSans', '//fonts.googleapis.com/css?family=Open+Sans:400,600,700,800' );
    wp_enqueue_style( 'OpenSans' );
}
add_action( 'wp_print_styles', 'google_fonts' );
```

## Modify Excerpt Length

```php
/**
 * Modify excerpt length
 */
 
function custom_excerpt_length( $length ) {
    return 25;
}
add_filter( 'excerpt_length', 'custom_excerpt_length', 999 );
```

## Change Read More Link

```php
/**
 * Change Read More link
 */
 
function custom_read_more_link() {
    return '<a href="' . get_permalink() . '">Read More</a>';
}
add_filter( 'the_content_more_link', 'custom_read_more_link' );
```

## Change More Excerpt

```php
/**
 * Change More excerpt
 */
 
function custom_more_excerpt( $more ) {
    return '...';
}
add_filter( 'excerpt_more', 'custom_more_excerpt' );
```

## Disable Emoji Mess

```php
/**
 * Disable Emoji mess
 */
 
function disable_wp_emojicons() {
    remove_action( 'admin_print_styles', 'print_emoji_styles' );
    remove_action( 'wp_head', 'print_emoji_detection_script', 7 );
    remove_action( 'admin_print_scripts', 'print_emoji_detection_script' );
    remove_action( 'wp_print_styles', 'print_emoji_styles' );
    remove_filter( 'wp_mail', 'wp_staticize_emoji_for_email' );
    remove_filter( 'the_content_feed', 'wp_staticize_emoji' );
    remove_filter( 'comment_text_rss', 'wp_staticize_emoji' );
    add_filter( 'tiny_mce_plugins', 'disable_emojicons_tinymce' );
    add_filter( 'emoji_svg_url', '__return_false' );
}
add_action( 'init', 'disable_wp_emojicons' );

function disable_emojicons_tinymce( $plugins ) {
    return is_array( $plugins ) ? array_diff( $plugins, array( 'wpemoji' ) ) : array();
}
```

## Remove Comments

```php
/**
 * Remove comments
 */
 
// Removes from admin menu

function my_remove_admin_menus() {
    remove_menu_page( 'edit-comments.php' );
}
add_action( 'admin_menu', 'my_remove_admin_menus' );

// Removes from post and pages
function remove_comment_support() {
    remove_post_type_support( 'post', 'comments' );
    remove_post_type_support( 'page', 'comments' );
}
add_action( 'init', 'remove_comment_support', 100 );

// Removes from admin bar
function mytheme_admin_bar_render() {
    global $wp_admin_bar;
    
    $wp_admin_bar->remove_menu( 'comments' );
}
add_action( 'wp_before_admin_bar_render', 'mytheme_admin_bar_render' );
```

## Change Media Gallery URL

```php
/**
 * Change Media Gallery URL
 */
 
if ( empty( get_option( 'upload_url_path' ) ) ) {
    update_option( 'upload_url_path', 'http://assets.website.com/wp-content/uploads' );
}
```

Also, you can filter the option value before it's retrieved from the database, which is slightly better:

```php
/**
 * Change Media Gallery URL
 */
 
add_filter( 'pre_option_upload_url_path', function() {
    return 'http://assets.website.com/wp-content/uploads';
});
```

## Create Custom Thumbnail Size

```php
/**
 * Create custom thumbnail size
 */
 
add_image_size( 'custom-thumbnail', 250, 250, true );
```

**Retrieve Thumbnail**

 ```php
 $thumb = wp_get_attachment_image_src( get_post_thumbnail_id($post->ID), 'custom-thumbnail' );

 echo $thumb[0]; 
 ```
 
Since WordPress 4.4.0, you can use:

```php
the_post_thumbnail_url( $size );
```

## Add Categories for Attachments

```php
/**
 * Add categories for attachments
 */
 
function add_categories_for_attachments() {
    register_taxonomy_for_object_type( 'category', 'attachment' );
}
add_action( 'init' , 'add_categories_for_attachments' );
```

## Add Tags for Attachments

```php
/**
 * Add tags for attachments
 */
 
function add_tags_for_attachments() {
    register_taxonomy_for_object_type( 'post_tag', 'attachment' );
}
add_action( 'init' , 'add_tags_for_attachments' );
```

## Add Custom Excerpt to Pages

```php
/**
 * Add custom excerpt to pages
 */
 
function add_page_excerpt() {
    add_post_type_support( 'page', array( 'excerpt' ) );
}
add_action( 'init', 'add_page_excerpt' );
```

## Create a Global String

```php
/**
 * Create a global string
 */
 
function global_string() {
    return 'String';
}
```

**Retrieve Field**

```php
echo global_string();
```

## Support Featured Images

```php
/**
 * Support featured images
 */
 
add_theme_support( 'post-thumbnails' );
```

## Support Search Form

```php
/**
 * Support search form
 */
 
add_theme_support( 'html5', array( 'search-form' ) );
```

## Excluding Pages From Search

```php
/**
 * Excluding pages from search
 */
 
function exclude_pages_from_search() {
    global $wp_post_types;

    $wp_post_types['page']->exclude_from_search = true;
}
add_action( 'init', 'exclude_pages_from_search' );
```

## Disable xmlrpc.php

```php
/**
 * Disable xmlrpc.php
 */
 
add_filter( 'xmlrpc_enabled', '__return_false' );
remove_action( 'wp_head', 'rsd_link' );
remove_action( 'wp_head', 'wlwmanifest_link' );
```

## Escape HTML in Posts

```php
/**
 * Escape HTML in <code> or <pre><code> tags.
 */
 
function escapeHTML($arr) {
    if (version_compare(PHP_VERSION, '5.2.3') >= 0) {
        $output = htmlspecialchars($arr[2], ENT_NOQUOTES, get_bloginfo('charset'), false);
    }
    else {
        $specialChars = array(
            '&' => '&amp;',
            '<' => '&lt;',
            '>' => '&gt;'
        );

        // decode already converted data
        $data = htmlspecialchars_decode( $arr[2] );
        // escape all data inside <pre>
        $output = strtr( $data, $specialChars );
    }
    if (! empty($output)) {
        return  $arr[1] . $output . $arr[3];
    }    else     {
        return  $arr[1] . $arr[2] . $arr[3];
    }
}
function filterCode($data) { // Uncomment if you want to escape anything within a <pre> tag
    //$modifiedData = preg_replace_callback( '@(<pre.*>)(.*)(<\/pre>)@isU', 'escapeHTML', $data );
    $modifiedData = preg_replace_callback( '@(<code.*>)(.*)(<\/code>)@isU', 'escapeHTML', $data );
    $modifiedData = preg_replace_callback( '@(<tt.*>)(.*)(<\/tt>)@isU', 'escapeHTML', $modifiedData );

    return $modifiedData;
}
add_filter( 'content_save_pre', 'filterCode', 9 );
add_filter( 'excerpt_save_pre', 'filterCode', 9 );
```

Modified from [Escape HTML](https://wordpress.org/plugins/escape-html/).

## Create Custom Global Settings

```php
/**
 * Create custom global settings
 */
 
function custom_settings_page() { ?>
    <div class="wrap">
    <h1>Custom Settings</h1>
    <form method="post" action="options.php">
        <?php
            settings_fields( 'section' );
            do_settings_sections( 'theme-options' );
            submit_button();
        ?>
    </form>
    </div>
<?php }

function custom_settings_add_menu() {
    add_theme_page( 'Custom Settings', 'Custom Settings', 'manage_options', 'custom-settings', 'custom_settings_page', null, 99 );
}
add_action( 'admin_menu', 'custom_settings_add_menu' );

// Example setting
function setting_twitter() { ?>
    <input type="text" name="twitter" id="twitter" value="<?php echo get_option('twitter'); ?>" />
<?php }

function custom_settings_page_setup() {
    add_settings_section( 'section', 'All Settings', null, 'theme-options' );
    add_settings_field( 'twitter', 'Twitter Username', 'setting_twitter', 'theme-options', 'section' );
    register_setting( 'section', 'twitter' );
}
add_action( 'admin_init', 'custom_settings_page_setup' );
```

Retrieve Field

```php
echo get_option( 'twitter' );
```

Modified from [Create a WordPress Theme Settings Page with the Settings API](http://www.sitepoint.com/create-a-wordpress-theme-settings-page-with-the-settings-api/).

## Remove WordPress Admin Bar

```php
/**
 * Remove WordPress admin bar
 */

function remove_admin_bar() {
    remove_action( 'wp_head', '_admin_bar_bump_cb' );
}
add_action( 'get_header', 'remove_admin_bar' );
```

## Add Open Graph Meta Tags

```php
/**
 * Add Open Graph Meta Tags
 */

function meta_og() {
    global $post;

    if ( is_single() ) {
        if( has_post_thumbnail( $post->ID ) ) {
            $img_src = wp_get_attachment_image_src( get_post_thumbnail_id( $post->ID ), 'thumbnail' );
        } 
        $excerpt = strip_tags( $post->post_content );
        $excerpt_more = '';
        if ( strlen($excerpt ) > 155) {
            $excerpt = substr( $excerpt,0,155 );
            $excerpt_more = ' ...';
        }
        $excerpt = str_replace( '"', '', $excerpt );
        $excerpt = str_replace( "'", '', $excerpt );
        $excerptwords = preg_split( '/[\n\r\t ]+/', $excerpt, -1, PREG_SPLIT_NO_EMPTY );
        array_pop( $excerptwords );
        $excerpt = implode( ' ', $excerptwords ) . $excerpt_more;
        ?>
<meta name="author" content="Your Name">
<meta name="description" content="<?php echo $excerpt; ?>">
<meta property="og:title" content="<?php echo the_title(); ?>">
<meta property="og:description" content="<?php echo $excerpt; ?>">
<meta property="og:type" content="article">
<meta property="og:url" content="<?php echo the_permalink(); ?>">
<meta property="og:site_name" content="Your Site Name">
<meta property="og:image" content="<?php echo $img_src[0]; ?>">
<?php
    } else {
        return;
    }
}
add_action('wp_head', 'meta_og', 5);
```

## Add Custom Post Type

```php
/**
 * Add custom post type
 */

function create_custom_post() {
    register_post_type( 'custom-post', // slug for custom post type
        array(
        'labels' => array(
            'name' => __( 'Custom Post' ),
        ),
        'public' => true,
        'hierarchical' => true, 
        'has_archive' => true,
        'supports' => array(
            'title',
            'editor',
            'excerpt',
            'thumbnail'
        ), 
        'can_export' => true,
        'taxonomies' => array(
                'post_tag',
                'category'
        )
    ));
}
add_action('init', 'create_custom_post');
```

## Implement Preconnect to Google Fonts in Themes

```php
/**
 * Implement preconnect to Google Fonts in themes
 */

function twentyfifteen_resource_hints( $urls, $relation_type ) {
    // Checks whether the subject is carrying the source of fonts google and the `$relation_type` equals preconnect.
    // Replace `enqueue_font_id` the `ID` used in loading the source.
    if ( wp_style_is( 'enqueue_font_id', 'queue' ) && 'preconnect' === $relation_type ) {
        // Checks whether the version of WordPress is greater than or equal to 4.7
        // to ensure compatibility with older versions
        // because the 4.7 has become necessary to return an array instead of string
        if ( version_compare( $GLOBALS['wp_version'], '4.7-alpha', '>=' ) ) {
            // Array with url google fonts and crossorigin
            $urls[] = array(
                'href' => 'https://fonts.gstatic.com',
                'crossorigin',
            );
        } else {
            // String with url google fonts
            $urls[] = 'https://fonts.gstatic.com';
        }
    }
    return $urls;
}
add_filter( 'wp_resource_hints', 'twentyfifteen_resource_hints', 10, 2 ); 
```

## Add Thumbnail Column to Post Listing

```php
/**
 * Add thumbnail column to post listing
 */

add_image_size( 'admin-list-thumb', 80, 80, false );

function wpcs_add_thumbnail_columns( $columns ) {
     
    if ( !is_array( $columns ) )
        $columns = array();
    $new = array();

    foreach( $columns as $key => $title ) {
        if ( $key == 'title' ) // Put the Thumbnail column before the Title column
            $new['featured_thumb'] = __( 'Image');
        $new[$key] = $title;
    }
    return $new;
}

function wpcs_add_thumbnail_columns_data( $column, $post_id ) {
    switch ( $column ) {
    case 'featured_thumb':
        echo '<a href="' . $post_id . '">';
        echo the_post_thumbnail( 'admin-list-thumb' );
        echo '</a>';
        break;
    }
}

if ( function_exists( 'add_theme_support' ) ) {
    add_filter( 'manage_posts_columns' , 'wpcs_add_thumbnail_columns' );
    add_action( 'manage_posts_custom_column' , 'wpcs_add_thumbnail_columns_data', 10, 2 );
}
```
## Add Lead Class to First Paragraph

```php
/**
 * Add lead class to first paragraph
 */

function first_paragraph( $content ) {
    return preg_replace( '/<p([^>]+)?>/', '<p$1 class="lead">', $content, 1 );
}
add_filter( 'the_content', 'first_paragraph' );
```

Adds a `lead` class to the first paragraph in [the_content](https://developer.wordpress.org/reference/functions/the_content/).

## Exclude Custom Post Type from Search

```php
/**
 * Exclude custom post type from search
 */

function excludePages( $query ) {
if ( $query->is_search ) {
    $query->set( 'post_type', 'post' );
}
    return $query;
}
add_filter( 'pre_get_posts','excludePages' );
```

## Remove Query String from Static Resources

```php
/**
 * Remove query string from static resources 
 */
 
function remove_cssjs_ver( $src ) {
    if ( strpos( $src, '?ver=' ) )
        $src = remove_query_arg( 'ver', $src );
    return $src;
}
add_filter( 'style_loader_src', 'remove_cssjs_ver', 10, 2 );
add_filter( 'script_loader_src', 'remove_cssjs_ver', 10, 2 );
```

## Modify jQuery

```php
/**
 * Modify jQuery
 */

function modify_jquery() {
    wp_deregister_script( 'jquery' );
    wp_register_script( 'jquery', 'https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js', false, '3.2.1' );
    wp_enqueue_script( 'jquery' );
}
if (!is_admin()) add_action('wp_enqueue_scripts', 'modify_jquery');
```

##  Disable Website Field From Comment Form

```php
/** 
 * Disable website field from comment form
 */

function disable_website_field( $field ) { 
    if( isset($field['url']) ) {
        unset( $field['url'] );
    }
    return $field;
}
add_filter('comment_form_default_fields', 'disable_website_field');
```

##  Disable JSON REST API

```php
/** 
 * Disable JSON REST API  
 */

add_filter('json_enabled', '__return_false');
add_filter('json_jsonp_enabled', '__return_false');
```

## Switch Post Type

```php
/**
 * Switch post type
 */

function switch_post_type ( $old_post_type, $new_post_type ) {
    global $wpdb;

    // Run the update query
    $wpdb->update(
        $wpdb->posts,
        // Set
        array( 'post_type' => $new_post_type),
        // Where
        array( 'post_type' => $old_post_type )
    );
}
```

## PHP Logger

```php
/**
 * PHP Logger
 */

function php_logger( $data ) {
    $output = $data;
    if ( is_array( $output ) )
        $output = implode( ',', $output );
        
    // print the result into the JavaScript console
    echo "<script>console.log( 'PHP LOG: " . $output . "' );</script>";
}
```

## Always Show Second Bar in TinyMCE

```php
/**
 * Always show second bar in TinyMCE
 */

function show_tinymce_toolbar( $in ) {
    $in['wordpress_adv_hidden'] = false;
    return $in;
}
add_filter( 'tiny_mce_before_init', 'show_tinymce_toolbar' );
```

## Remove Admin Menu Items Depending on User Role

```php
/**
 * Clone the administrator user role
 */

function clone_admin_role() {
    global $wp_roles;
    if ( ! isset( $wp_roles ) )
        $wp_roles = new WP_Roles();
    
    $adm = $wp_roles->get_role( 'administrator' );
    
    // Add new "Client" role with all admin capabilities
    $wp_roles->add_role( 'client', 'Client', $adm->capabilities );
}
add_action( 'init', 'clone_admin_role' );

/**
 * Specify which admin menu items are visible for users with role "Client"
 */

function remove_dashboard_menus() {
    if ( current_user_can( 'client' ) ) {
        // Hide Updates under Dashboard menu
        remove_submenu_page( 'index.php', 'update-core.php' );

        // Hide Comments
        remove_menu_page( 'edit-comments.php' );

        // Hide Plugins
        remove_menu_page( 'plugins.php' );

        // Hide Themes, Customizer and Widgets under Appearance menu
        remove_submenu_page( 'themes.php', 'themes.php' );
        remove_submenu_page( 'themes.php', 'customize.php?return=' . urlencode( $_SERVER['REQUEST_URI'] ) );
        remove_submenu_page( 'themes.php', 'widgets.php' );

        // Hide Tools
        remove_menu_page( 'tools.php' );

        // Hide General Settings
        remove_menu_page( 'options-general.php' );
    }
}
add_action( 'admin_menu', 'remove_dashboard_menus' );
```

## Remove Admin Menu Items Depending on Email Address (domain)

```php
/**
 * Specify which users can see admin menu items based on their email address
 */

function remove_dashboard_menus() {
    $user_data = get_userdata( get_current_user_id() );
    $user_email = isset( $user_data->user_email ) ? $user_data->user_email : '';

    if ( ! strpos( $user_email, '@yourcompany.com' ) ) {
        // Hide Updates under Dashboard menu
        remove_submenu_page( 'index.php', 'update-core.php' );

        // Hide Comments
        remove_menu_page( 'edit-comments.php' );

        // Hide Plugins
        remove_menu_page( 'plugins.php' );

        // Hide Themes, Customizer and Widgets under Appearance menu
        remove_submenu_page( 'themes.php', 'themes.php' );
        remove_submenu_page( 'themes.php', 'customize.php?return=' . urlencode( $_SERVER['REQUEST_URI'] ) );
        remove_submenu_page( 'themes.php', 'widgets.php' );

        // Hide Tools
        remove_menu_page( 'tools.php' );

        // Hide General Settings
        remove_menu_page( 'options-general.php' );
    }
}
add_action( 'admin_menu', 'remove_dashboard_menus' );
```

## Reorder Admin Menu Items

```php
/**
 * Reorder admin menu
 */

function custom_menu_order( $menu_ord ) {
    if ( ! $menu_ord ) { return true; }
        return array(
            'index.php',
            'separator1',
            'edit.php?post_type=page', 
            'edit.php', 
            'edit.php?post_type=[your_post_type_slug]',
            'upload.php',
            'edit-comments.php',
            'separator2',
            'themes.php',
            'plugins.php',
            'users.php',
            'tools.php',
            'options-general.php'
        );
    }
}
add_filter( 'custom_menu_order', 'custom_menu_order' );
add_filter( 'menu_order', 'custom_menu_order' );
```

## Exclude a Category From WordPress Loops

```php
/**
 * Exclude a category from all WordPress loops
 */

add_action( 'pre_get_posts', function( $query ) { // anonymous callback
    
    global $wp_query; 

    // Hard coded category ID, but can be dynamic: esc_attr(get_option('your-cat-id')); 
    $excluded_cat_id = 25;

    // add category ID to existing, avoid overwriting it 
    $cat[] = $query->get( 'cat' );
    $cat[] = "-" . $excluded_cat_id;

    $query->set( 'cat', $cat );
    }
});
```

## Disable the message - JQMIGRATE: Migrate is installed, version 1.4.1

```php
add_action('wp_default_scripts', function ($scripts) {
    if (!empty($scripts->registered['jquery'])) {
        $scripts->registered['jquery']->deps = array_diff($scripts->registered['jquery']->deps, ['jquery-migrate']);
    }
});
```

## Load heavy 3rd-party scripts later for better performance

Lighthouse and similar performance analysis tools always complain about render-blocking scripts (and styles),
short cache TTL etc. Most of these scripts and styles come from 3rd-party sources which we can't control –
Google's own Tag Manager and Analytics, Facebook Pixel, other trackers and chat scripts etc. However, we
can load them only when a real user interacts with a page, significantly reducing the Time To Interactive
metric and scoring much higher performance results.

Depending on where you like these 3rd-party scripts to be, you can either use `wp_footer` action to print the
code in footer, or put it in your main `app.js` script which, in turn, is enqueued on `wp_enqueue_scripts` action.

```javascript
<script>
var fired = false;

window.addEventListener('scroll', () => {
    if (fired === false) {
        fired = true;
        
        setTimeout(() => {

            // Marketing scripts go here.

        }, 1000) // 1000ms or 1s works fine, but you can adjust this timeout.
    }
});
</script>
```

# Adds not-home class to body
## Adds .not-home to all pages except for homepage

```php
/**
 * Adds not-home class to body
 */
function add_not_home_body_class($classes) {
    if( !is_front_page() ) $classes[] = 'not-home';
    return $classes;
}
add_filter('body_class','add_not_home_body_class');
```


# Use Relevanssi search instead of the default
## Relevanssi search plugin needs to be installed

```php
/**
 * Use Relevanssi in search instead of the default search
 */
add_filter('avf_ajax_search_function', 'avia_init_relevanssi', 10, 4);
function avia_init_relevanssi($function_name, $search_query, $search_parameters, $defaults) {
    $function_name = 'avia_relevanssi_search';
    return $function_name;
}
function avia_relevanssi_search($search_query, $search_parameters, $defaults) {
    global $query;
    $tempquery = $query;
    if(empty($tempquery)) $tempquery = new WP_Query();

    $tempquery->query_vars = $search_parameters;
    relevanssi_do_query($tempquery);
    $posts = $tempquery->posts;

    return $posts;
}
```

# Solves HTTP ERROR when uploading media
## WordPress runs on PHP which uses two modules to handle images. These modules are called GD Library and Imagick. WordPress may use either one of them depending on which one is available. However, Imagick is known to often run into memory issues causing the http error during image uploads. To fix this, you can make the GD Library your default image editor.

```php
/**
 * Solves HTTP ERROR when uploading media
 */
function wpb_image_editor_default_to_gd( $editors ) {
    $gd_editor = 'WP_Image_Editor_GD';
    $editors = array_diff( $editors, array( $gd_editor ) );
    array_unshift( $editors, $gd_editor );
    return $editors;
}
add_filter( 'wp_image_editors', 'wpb_image_editor_default_to_gd' );
```

# Hides empty categories in products category widget
```php
/**
 * Hides empty categories in products category widget
 */
function woo_hide_product_categories_widget( $list_args )
{
    $list_args[ 'hide_empty' ] = 1;
    return $list_args;
}
add_filter( 'woocommerce_product_categories_widget_args', 'woo_hide_product_categories_widget' );
```

# Adds post category to the body-class
```php
/**
 * Adds post category to the the body_class
 */
function category_id_class($classes) {
    global $post;
    foreach((get_the_category($post->ID)) as $category)
        $classes[] = $category->category_nicename;
    return $classes;
}
add_filter('body_class', 'category_id_class');
```

# Changes the text in Thank you page after checkout on Woocommerce
```php
/**
 * Changes the text in Thank you page after checkout (Woocommerce)
 */
add_filter( 'woocommerce_thankyou_order_received_text', 'avia_thank_you' );
function avia_thank_you() {
 $added_text = '<p>Thank you for your order. You will receive an email shortly with more information.</p>';
 return $added_text ;
}
```

# Points the event link to the event website URL in The Events Calendar plugin
## Simply Comment out the add_filter() line to disable this function.
```php
/**
 * Changes the event link to the event website URL if that is set.
 */
add_filter( 'woocommerce_thankyou_order_received_text', 'avia_thank_you' );
function avia_thank_you() {
 $added_text = '<p>Thank you for your order. You will receive an email shortly with more information.</p>';
 return $added_text ;
}
```

# Activates header extra widget area in Enfold
```php
/**
 * Activates Header extra widget area (Enfold theme)
 */
add_action( 'ava_after_main_menu', 'enfold_customization_header_widget_area' );
function enfold_customization_header_widget_area() {
    dynamic_sidebar( 'header' );
}
```

# Disables portfolio items in Enfold
```php
/**
 * Disables portfolio items (Enfold theme)
 */
add_action( 'after_setup_theme', 'remove_portfolio' );
function remove_portfolio() {
    remove_action( 'init', 'portfolio_register' );
}
```

# Adds custom post type to avia builder in Enfold
```php
/**
 * Adds custom post type to avia builder (Custom Post Types plugin & Enfold theme)
 */
add_theme_support('add_avia_builder_post_type_option');
add_theme_support('avia_template_builder_custom_post_type_grid');
```

# Activates Advanced Layout Builder on Custom Post types in Enfold
```php
/**
 * Activates Advanced Layout Builder on Custom Post types (Custom Post Types plugin & Enfold theme)
 */
function avf_alb_supported_post_types_mod( array $supported_post_types ) {
  $supported_post_types[] = 'template';
  return $supported_post_types;
}
add_filter('avf_alb_supported_post_types', 'avf_alb_supported_post_types_mod', 10, 1);

function avf_metabox_layout_post_types_mod( array $supported_post_types ) {
 $supported_post_types[] = 'template';
 return $supported_post_types;
}
add_filter('avf_metabox_layout_post_types', 'avf_metabox_layout_post_types_mod', 10, 1);

add_theme_support('avia_template_builder_custom_post_type_grid');
add_theme_support('add_avia_builder_post_type_option');
```

# Hides web field from comment form
```php
/**
 * Hides web field from comment form
 */
add_filter('comment_form_default_fields', 'website_remove');
function website_remove($fields) {
    if(isset($fields['url']))
    unset($fields['url']);
    return $fields;
}
```

# Fixes buggy view in events tribe plugin list admin table
```php
/**
 * Fixes buggy view in events tribe plugin list admin table
 */
add_action('admin_head', 'my_custom_fonts');

function my_custom_fonts() {
  echo '<style>
	table.fixed {
	  table-layout: auto !important;
	}
	.avia-template-save-button-container {
	  position: relative !important;
	  float: right !important;
	  top: 40px !important;
	}
  </style>';
}
```

# Removes items from WP admin toolbar
```php
/**
 * Removes items from WP admin toolbar
 */
// Remove items from the admin bar
function remove_from_admin_bar($wp_admin_bar) {
    /*
     * Placing items in here will only remove them from admin bar
     * when viewing the fronte end of the site
    */
    if ( ! is_admin() ) {
        // Example of removing item generated by plugin. Full ID is #wp-admin-bar-si_menu
        $wp_admin_bar->remove_node('si_menu');
 
        // WordPress Core Items (uncomment to remove)
        $wp_admin_bar->remove_node('updates');
        $wp_admin_bar->remove_node('comments');
        $wp_admin_bar->remove_node('new-content');
        $wp_admin_bar->remove_node('wp-logo');
		$wp_admin_bar->remove_node('wp-mail-smtp-menu');
        //$wp_admin_bar->remove_node('site-name');
        //$wp_admin_bar->remove_node('my-account');
        $wp_admin_bar->remove_node('search');
        $wp_admin_bar->remove_node('customize');
    }
 
    /*
     * Items placed outside the if statement will remove it from both the frontend
     * and backend of the site
    */
    $wp_admin_bar->remove_node('wp-logo');
}
add_action('admin_bar_menu', 'remove_from_admin_bar', 999);
```