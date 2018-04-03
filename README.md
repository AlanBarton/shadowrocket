# shadowrocket

A composer component that helps you to build your own socket tunnel.

[中文文档](doc/README-chn.md)

## Features
1. TCP/UDP support
2. IPV4/DOMAINNAME/IPV6 support
3. monolog support

### Coming Next
- black list
- server manager
- user management


## Install

    composer require ycgambo/shadowrocket

### Requirements
1. Composer
2. PHP 5.3+

## Usage

### Run a server

```php
<?php
require_once __DIR__ . '/vendor/autoload.php';

use ShadowRocket\Bin\Launcher;

Launcher::initialize();
Launcher::addModule('server');
Launcher::launchAll();
```

These code start a server by using default configurations.

### Custom configuration

```php
<?php
require_once __DIR__ . '/vendor/autoload.php';

use ShadowRocket\Bin\Launcher;

$config = array(
    'server' => array(
        'port'        => '8388',
        'password'    => 'mypass',
        'encryption'  => 'aes-256-cfb',
        'process_num' => 12,
    )
);
Launcher::initialize($config);
Launcher::addModule('server');

// change some server configurations to config another port
Launcher::addModule('server', $changing_config = array(
    'port'        => '8389',
    'password'    => 'another_pass'
));

// launch these two servers
Launcher::launchAll();
```

### Run a local proxy

```php
<?php
require_once __DIR__ . '/vendor/autoload.php';

use ShadowRocket\Bin\Launcher;

$config = array(
    'local' => array(
        'server'      => '123.456.78.9',
        'port'        => '8388',
        'password'    => 'mypass',
        'encryption'  => 'aes-256-cfb',
        'local_port'  => '1086',
        'process_num' => 12,
    )
);
Launcher::initialize($config);
Launcher::addModule('local');
Launcher::launchAll();
```

Now we can pass data to 127.0.0.1:1086 and server 123.456.78.9:8388 will reply.

## Want a client APP?

- [For Android](https://github.com/shadowsocks/shadowsocks-android/releases)
- [For IOS](https://itunes.apple.com/cn/app/superwingy/id1290093815?mt=8)
- [For Mac](https://github.com/shadowsocks/ShadowsocksX-NG/releases) 
- [For Windows](https://github.com/shadowsocks/shadowsocks-windows/releases)
