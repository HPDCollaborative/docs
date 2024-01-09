---
title: API Libraries
description: Discussion of libraries required for using the HPDC API.
---

[[toc]]

# Libraries {.doc-heading}

The HPDC API is built on Laravel 5.6, and uses OAuth 2\* for authentication, thusly, the first library we've built is a simple authentication SDK written in PHP for implementing authentication to access your HPDC Builder account.

You can find the SDK on our GitHub account: [HPDCollaborative/php-sdk](https://github.com/HPDCollaborative/php-sdk)

::: danger required
**YOU MUST BE AN EXISTING API PARTNER TO USE THE API**
:::

Once you've received access to the API as a Partner, you can then begin integrating OAuth2 authentication and token access with this SDK, or you can roll your own using the SDK as a guide.

## Installation {.doc-heading}

The SDK uses composer to manage dependencies so you'll need to ensure you have a working knowledge of composer to install and integrate it into your application.

To install the SDK run:

```bash

composer require hpdc/sdk
```

This will download the SDK into your vendor directory and set up autoloading with the PSR-4 autoloading convention.

## Usage {.doc-heading}

The SDK uses [Guzzle](https://github.com/guzzle/guzzle) to create a CURL client and properly formatted PSR-7 messages, if you're rolling your own SDK in a different language, feel free to implement whichever CURL wrapper works best for you.

The SDK requires 3 specific configuration options which you must provide using the built in setters.

1. API Url (either the dev url for testing, or the production url for live apps)
2. Your Application ID
3. Your Application Secret

The SDK constructor creates an instance of the GuzzleHttp/Client. So you can do something like this in your implementation:

```php
<?php

use Hpdc\Authentication;

protected $client;

public function __construct()
{
	$this->client = new Authentication();
}
```

If available in your application framework, you can also type hint the Authentication class and set that to your property like so:

```php
<?php

public function __construct(Authentication $auth)
{
	$this->client = $auth;
}
```

The setters in the SDK are chainable, so you can now set your configuration variables by chaining them onto your existing `client` instance:

```php
<?php

// Url choices are:
// Development/Testing: https://dev.api.hpd-collaborative.org
// Production: https://api.hpd-collaborative.org

$this->client->setUrl('https://dev.api.hpd-collaborative.org')
			 ->setCallback('https://yoursite.com/callback')
			 ->setClient('your-client-id')
			 ->setSecret('your-client-secret');
```

Once you've set your configuration variables, you can then make OAuth calls to the API to retrieve codes and tokens.

First, retrieve an authorization code:

```php
<?php

// retrieve your auth code from the api
$url = $this->client->make();

// redirect your users to your callback url
return redirect($url);
```

Now you can retrieve a token and set that into your current session:

```php
<?php

// code variable returned from OAuth
// capture this from your request object
$code = $request->code;

// retrieve your token
$response = $this->client->send($code);

// store the token in your session
session(['api'       => $response]);
session(['api-token' => $response['access_token']]);

return redirect('/');
```

Obviously you'll need to adjust this for use in your framework, but you should now be ready to make requests to your HPDC Builder account via the API.

Keep in mind that you'll want to make sure that the session variables you set in your callback are removed when the user logs out. Something similar to this, adjusted for your framework:

```php
<?php

public function forget()
{
	// remove API token from session.
	session()->forget('api-token');
    session()->forget('api');

    return redirect('/');
}
```
