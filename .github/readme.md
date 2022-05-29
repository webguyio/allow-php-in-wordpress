# allow php in wordpress

```php
// allow php in content areas
add_filter( 'the_content', 'blank_php', 100 );
function blank_php( $html ) {
    if ( get_page_template_slug() == 'templates/blank.php' || get_page_template_slug() == 'templates/creative.php' ) {
        if ( strpos( $html, '<' . '?php' ) !== false ) {
            ob_start();
            eval( '?' . '>' . $html );
            $html = ob_get_contents();
            ob_end_clean();
        }
        return $html;
    }
}
```
