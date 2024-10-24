# WooFood Plugin

WooFood is a powerful plugin that allows restaurants to create an online food ordering system with ease. Below are some code snippet examples to help you extend or tweak WooFood’s functionality.

For more details on WooFood, visit the [official WooFood page](https://www.wpslash.com/plugin/woofood-food-delivery-plugin).

## Code Snippets

You can extend or customize WooFood by adding code snippets to your theme's `functions.php` file or by creating a custom plugin. Below are some examples.
### Replace Product Title with SKU on Automatic Printing Software
```php

add_filter('woofood_rest_line_item_name', 'woofood_hook_replace_title_with_sku', 10, 2);

function woofood_hook_replace_title_with_sku($product_name, $product_id)
{
    global $woocommerce;
    return wc_get_product($product_id)->get_sku();

}

```
