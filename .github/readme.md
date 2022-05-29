# Allow PHP in WordPress

https://wordpress.org/plugins/blank/ — I wanted to enable PHP in this plugin, which I think would make it far more useful. However, due to security concerns (which I understand), the WordPress admins are simply no longer accepting such features in new plugin submissions, so it had to be removed.

Of course, you, the individual user, has every right to manually add the functionality back in if you so wish.

Simply paste the following at the bottom of *blank.php*:

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

Or, if you're not even a user of the plugin, here's something more generic you can simply paste into your theme's *functions.php* file:

```php
add_filter( 'the_content', 'yourtheme_php', 100 );
function yourtheme_php( $html ) {
	if ( strpos( $html, '<' . '?php' ) !== false ) {
		ob_start();
		eval( '?' . '>' . $html );
		$html = ob_get_contents();
		ob_end_clean();
	}
	return $html;
}
```
