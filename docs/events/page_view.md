# Page View

Fire whenever a user loads in a new page, whether that is done synchronously or asynchronously.

This event should be the first pushed into the data layer on each page. Given many 3rd party scripts push events to the data layer, this event push should be placed in the page `<head>` and should be the first `<script>` tag on the page to ensure it is the first event.

???+ note "Page Views and Virtual Page Views are now the same in GA4"

    There is no longer a concept of virtual page view, so this event should be fired whenever a virtual page view would have been fired in the past, such as when a new screen is loaded asynchronously within an angular, react, or vue app/embed.

## Javascript Code

```js
// When:
// User loads a new page (synchronously or asynchronously)
// Should be the first push into dataLayer, placed in the <head> and ideally first <script> on page.

// Code
window.dataLayer = window.dataLayer || [];
dataLayer.push({ page_data: null, user_data: null });  // Clear the previous attributes.
dataLayer.push({
  event: 'page_view',
  page_data: {
    page_category: '<category>', // REQUIRED | string | ex. sun protection
    page_subcategory: '<page_subcategory>', // contextual | string | ex. waterproof
    page_id: '<page_id>', // REQUIRED | string | ex. 12345
    page_name: '<page_name>', // REQUIRED | string | ex. homepage, search results, product:sample
    page_type: '<page_type>', // REQUIRED | string | ex. article, blog, homepage, product
    site_brand: '<site_brand>', // REQUIRED | string | ex. neutrogena
    site_country: '<site_country>', // REQUIRED | string | ex us, au, is, jp
    site_franchise: '<site_franchise>', // REQUIRED | string | ex essential health, skin care & self care
    site_region: '<site_region>', // REQUIRED | string | ex. EMEA
    site_section: '<site_section>', // REQUIRED | string | ex. products
    user_login_state: '<user_login_state>' // REQUIRED | string | ex. authenticated, anonymous 
  },
  user_data: {
    user_id: '<user_id>' // REQUIRED, if user is logged in | string | ex. 12345
  }
});
```

## Variable Definitions

|Field|Type|Required|Description|Example|Max Length|
| --- | --- | --- | --- | --- | --- |
|**page_category**|`string`|required|Used for grouping pages (or screens) into categories based on their content. Most often aligns with page tags/taxonomy terms or breadcrumbs.|`sun protection`|`100`|
|**page_subcategory**|`string`|recommended|Used for grouping pages (or screens) into subcategories based on their content. Most often aligns with page tags/taxonomy terms or breadcrumbs.|`waterproof`|`100`|
|**page_id**|`string`|required|A durable identifier for a page that will enable measurement over time despite the page URL, title, etc changing. Generally sourced from the site content management system.|`12345`|`100`|
|**page_name**|`string`|required|A unique name for this page independent of page title. Google does not tend to use custom page names, but it's a mainstay in Adobe and therefore is included here for compatibility as well as for its usefulness generally.|`homepage,search results,product:neutrogena hydro boost ge`l|`100`|
|**page_type**|`string`|required|Used for grouping pages (or screens) into high level types.|`article,blog,homepage,product`|`100`|
|**site_brand**|`string`|required|The brand the site is associated with. <br /> <br />Please view the [Internal Documentation -  Product Hierarchy Mapping](https://prodbitabcon.jnj.com/#/site/Consumer/views/GlobalConsumerCommercialHierarchies/ProductHierarchyMappings?:iid=2) for additional definitions.|`neutrogena`|`100`|
|**site_country**|`string`|required|The country the site is associated with.<br /><br /> You _**must**_ use the [ISO Standard ==> Alpha-2-Codes](https://www.iso.org/iso-3166-country-codes.html).|`us`|`100`|
|**site_franchise**|`string`|required|The franchise the site is associated with. <br /> <br />Please view the [Internal Documentation -  Product Hierarchy Mapping](https://prodbitabcon.jnj.com/#/site/Consumer/views/GlobalConsumerCommercialHierarchies/ProductHierarchyMappings?:iid=2) for additional definitions.|`essential health, skin care & self care`|`100`|
|**site_region**|`string`|required|The region the site is associated with. <br /> <br />Please view the [Internal Documentation - Customer Mapping](https://prodbitabcon.jnj.com/#/site/Consumer/views/GlobalConsumerCommercialHierarchies/CustomerMappings?:iid=1) for additional definitions.|`EMEA`|`100`|
|**site_section**|`string`|required|The section of the site that the current page resides in.|products|100|
|**user_login_state**|`string`|required|Set on all events with the authentication status of the visitor.|`authenticated, anonymous`|`100`|
|**user_id**|`string`|contextual|The id of the user currently logged in to the site, if the site offers authentication and the user is authenticated.|`123456`|`100`|
