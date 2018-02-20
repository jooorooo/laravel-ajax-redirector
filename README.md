# laravel-ajax-redirector

A Laravel library for handling AJAX redirects

This package changes the redirect response for AJAX calls from 301 or 302 to a 278 JSON response. XHR requests follow
redirects which in a lot of cases, isn't the intention. In most cases, the intention is for the browser to redirect
the client to the intended page.

For **Laravel 4**, please use version 1.0.0.

For **Laravel 5**, please use version 2.0.0+

For **Laravel 5.6**, please use version 3.0.0+

## Installation

```bash
composer require simexis/laravel-ajax-redirector
```

After updating composer, add the service provider to the `providers` array in `config/app.php` for Laravel version < 5.5.*
```php
'providers' => [
    Superbalist\AjaxRedirector\AjaxRedirectServiceProvider::class,
]
```


## Usage

In your application, you'll continue to do redirects like you always have.
```php
return redirect()->to('/test');
```

In javascript, you'll need to watch for AJAX calls which result in HTTP 278 responses and do a client side redirect
using eg: window.location.replace(json.redirect_url);

With jQuery, this can be done using a Global AJAX Event Handler.

With AngularJS, this can be done using a $http interceptor.

The response from the server will look something like:
```
HTTP/1.1 278 unknown status
Content-Type: application/json

{"redirect_url":"http:\/\/your.site.com\/test"}
```
