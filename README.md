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

### Disable Coupon for Delivery Orders

```php

add_filter( 'woocommerce_coupon_is_valid', 'wpslash_hook_disable_coupon_code_for_delivery', 10, 3 );
function wpslash_hook_disable_coupon_code_for_delivery( $is_valid, $coupon, $discount ){
    if (!is_admin())
    {

   
    $coupon_code_to_apply = "YOURCOUPONCODEHERE";
    if($coupon == $coupon_code_to_apply)
    {
      if(WC()->session)
      {
        if (WC()->session->get( 'woofood_order_type') == "delivery")
      {
        return false;
      }
      }
      
    }
  }
  
    return $is_valid;
}

```

### Add Live Product Search on WooFood

```php

add_action("wp_footer", function()
{
	?>
	<style>
		input.woofood-live-search
		{
			width: 100%;
			margin-bottom: 10px;
			border: none;
			border: 1px solid #bdb0b0;
			padding: 10px;
		}
	</style>
	<script>
		jQuery(document).ready(function()
		{
			jQuery( "<input type='text' class='woofood-live-search' placeholder='Search for Products...'/> " ).insertBefore( ".woofood-accordion:first" )
			jQuery( "<div class='woofood-live-results'><ul class='woofood-products'></ul></div>" ).insertBefore( ".woofood-accordion:first" )

		});
		jQuery(document).on('propertychange input', '.woofood-live-search', function (e) {
			var valueChanged = false;
			var search_value = jQuery(this).val();
			var vthis = jQuery(this);
			if (search_value=="")
			{

				jQuery('.woofood-live-results .woofood-products').html("");
			}
			else
			{



				if (e.type=='propertychange') {
					valueChanged = e.originalEvent.propertyName=='value';
				} else {
					valueChanged = true;
				}
				if (valueChanged) {




				}
				jQuery('.woofood-live-results .woofood-products').html("");

				jQuery('.woofood-product-loop').each(function( index ) {
					console.log( index + ": " + jQuery( this ).find('.product-title span:first').text().toLowerCase() );
					if(jQuery( this ).find('.product-title span').text().toLowerCase().includes(search_value.toLowerCase()))
					{
						jQuery( this).clone().appendTo( ".woofood-live-results .woofood-products" );


					}
					else
					{
						


					}
				});
			}


		});

	</script>
	<?php



});

```
