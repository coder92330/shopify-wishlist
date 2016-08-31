# SHOPIFY WISHLIST

A set of Shopify files used to implement a user wishlist on a Shopify store using (S)CSS, Javascript, and Liquid. This implementation uses javascript's localStorage to maintain a user's product wishlist and does not require a user to be logged in to a customer account.

## Features

* Let users add products to a wishlist that can be viewed on a custom wishlist page
* Users do not need to be logged into a customer account
* Show which products have already been added to the user's wishlist on any page where wishlist buttons exist
* Have the wishlist page show a custom message if no items are currently in the user's wishlist
* Custom loading screen while the wishlist page populates

## Usage

To begin using the Shopify Wishlist copy the following files into your project directory:
* assets/Wishlist.js
* templates/page.wishlist.liquid
* snippets/product-tile.liquid
* snippets/wishlist-button.liquid

In order to add a product to a user's wishlist, there must be an element with a class of **wishlist-btn** with a data attribute **data-product-handle** that contains the handle of the product to be added. This can be found in the **wishlist-button.liquid** snippet file. See the very simple example below.

```
<div class="wishlist-btn" data-product-handle="{{ product.handle }}">Add To Wishlist</div>
```

If the user adds a product to wishlist the wishlist button element will have the class **is-active** added. The product handle from the element will be pushed to an array, converted to localStorage and saved. 

Any time a page is loaded, the **Wishlist.js** file will scan the page for any wishlist button elements that have a product handle matching those in the the localStorage array and automatically add the **is-active** class so that the user can see which products are already in their wishlist. 

If a user clicks on a wishlist button that is currently active, it will remove the corresponding product handle from the localStorage array, and remove the **is-active** class from that button.

To setup the custom wishlist page, create a new page called *wishlist* and set it's template to *page.wishlist* found in the **page.wishlist.liquid** file. Make sure the page handle is 'wishlist'. If you want to change this make sure to update the function *loadWishlist* in **Wishlist.js**. On the custom wishlist page, we will initially load every product in the shop and then run a scan to filter out any products that are not part of the wishlist. As some shop's may have many products, the **Wishlist.js** file will hide everything on the page except for a custom loading element until the scan is complete, at which point the loader will disappear and the wishlist items would populate.

