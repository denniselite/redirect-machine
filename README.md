# Redirector

This is a package for redirecting specific incoming requests to another resource.

### Config example

You should create `config.php` configuration file like this:

```php
return [
    
    // redirect user to target even route is not found in configuration
    'forceRedirect' => false,
    
    // target web-site domain for user redirecting
    'targetHost' => 'target-host.local',
    
    // key-value set, "link from current web-site" => "link to page on the new web-site"
    // every link should start with '/'
    'routes' => [
        '/some-article' => '/some-article-on-target'
    ]
];
```

where:

* forceRedirect - redirect user even route is not found in configuration
* targetHost - target web-site domain for user redirecting
* routes - key-value set, where __key__ is a link from current web-site and __value__ is a link to page on the new web-site

Warning! Keys and values for routes map should start with '/'! 

==============================================================

### Usage examples

##### Via composer
1. Add this into *composer.json*
```
    "repositories": [
        { "type": "vcs", "url": "https://github.com/denniselite/redirector"}
    ],
    "require": {
        "denniselite/redirector" : "dev-master"
    }
```

2. After that run `composer install` command and use it before the application running:
```php
(new \Redirector\Redirector)->setConfig($config)->run();
```

##### Without composer

If your project doesn't support the *composer* manager (wordpress, joomla, ...):

1. Init composer in your project directory using the `composer init` command;
2. Add in composer.json:

```
...
    "repositories": [
        { "type": "vcs", "url": "https://github.com/denniselite/redirector"}
    ],
    "require": {
        "denniselite/redirector" : "dev-master"
    }
...    
```

3. Run `composer install`;
4. Add into your start-script, e.g. index.php following code:

```php
require_once "vendor/autoload.php";
$config = require_once "config.example.php";
(new \Redirector\Redirector)->setConfig($config)->run();
```  

5. Done!


You also are able to use only zip-downloading mechanism for this package usage. For it you should import src files from package:

```php
require_once "Redirector/Redirector.php";
require_once "Redirector/IRedirectable.php";
$config = require_once "config.example.php";
(new \Redirector\Redirector)->setConfig($config)->run();
```

But it isn't convenient for version management and code supporting.

PPS Be careful about `vendor/` directory and configuration files - they should be hidden for HTTP requests ;)