CybozuHttpBundle[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](https://github.com/ochi51/CybozuHttpBundle/tree/master/LICENSE.md)
=======================

@todo badge

Symfony bundle that integrates the [Cybozu HTTP](https://github.com/ochi51/cybozu-http) by providing easy-to-use services and configuration.

cybozu.com API Documentation
------------

[Japanese](https://cybozudev.zendesk.com/hc/ja)
[English](https://developer.kintone.io/hc/en-us)

Requirements
------------

- PHP >=5.5
- Composer
- Symfony >=2.3

Installation
------------

The recommended way to install Cybozu HTTP is with [Composer](https://getcomposer.org/).
Composer is a dependency management tool for PHP that allows you to declare the dependencies your project needs and installs them into your project.

```{.bash}
    $ curl -sS https://getcomposer.org/installer | php
    $ mv composer.phar /usr/local/bin/composer
```

You can add Cybozu HTTP as a dependency using the composer

```{.bash}
    $ composer require ochi51/cybozu-http-bundle
```

Alternatively, you can specify Cybozu HTTP as a dependency in your project's existing composer.json file:

```{.json}
    {
       "require": {
          "ochi51/cybozu-http-bundle": "dev-master"
       }
    }
```

After installing, you need to register the bundle in your application.

```{.php}
    // app/AppKernel.php
    class AppKernel extends Kernel
    {
        // ...
        public function registerBundles()
        {
            $bundles = array(
                // ...
                new CybozuHttpBundle\CybozuHttpBundle()
            );
        }
    }
```

Configuration
------------

There are two ways that configure cybozu.com account information.

1. Add to `app/parameters.yml`.

```{.yml}
    # app/config.yml
    cybozu_http:
        domain:         cybozu.com
        subdomain:      changeMe
        useApiToken:    false
        login:          changeMe
        password:       changeMe
        token:          null
        useBasic:       false
        basicLogin:     null
        basicPassword:  null
        useClientCert:  false
        certFile:       /path/to/cert.pem
        certPassword:   null
        debug:          false
        logfile:        /path/to/logfile.log
```

2. User entity has it.

```{.yml}
    # app/config.yml
    cybozu_http:
        cert_dir:       /path/to/cert_dir
        logfile:        /path/to/logfile.log
```

```{.php}
    use CybozuHttpBundle\Entity\UserInterface;
    
    class User implements UserInterface
    {
        public function getCybozuHttpConfig()
        {
            return [
                "domain" =>         "cybozu.com",
                "subdomain" =>      "changeMe",
                "useApiToken" =>    false,
                "login" =>          "changeMe",
                "password" =>       "changeMe",
                "token" =>          null,
                "useBasic" =>       false,
                "basicLogin" =>     null,
                "basicPassword" =>  null,
                "useClientCert" =>  false,
                "certFile" =>       "cert.pem",
                "certPassword" =>   null
            ];
        }
        
        public function getDebugMode()
        {
            return true;
        }
    }
```

Quick example
------------

```{.php}
    <?php
    // AppBundle\Controller\MyCybozuHttpController
    
    public function getRecordAction($appId, $recordId)
    {
        $api = $this->get('cybozu_http.kintone_api_client');
        $record = $api->record()->get($appId, $recordId);
        // do something
    }
```


Testing
------------

To run the tests, Run the following command from the project folder.

```{.bash}
    $ php ./bin/phpunit
```

TODO
------------

- Japanese documentation.

License
------------

The MIT License (MIT). Please see [LICENSE](LICENSE) for more information.