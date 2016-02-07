MToolkit
========
The PHP framework to write less and do more.

#Summary
- [Landing page](http://mtoolkit.github.io/mtoolkit/)
- [Intro](#into)
- [Some good features](#some_good_features)
- [Install](#install)
- [MToolkit modules](#mtoolkit_modules)
- [Software using MToolkit](#software_using_mtoolkit)
- [Let's start](#lets_start)

#<a name="intro"></a>Intro

MToolkit is a simple PHP toolkit, it is compliant with the PSR-4 Standard:
- A fully qualified class name has the following form: \<NamespaceName>(\<SubNamespaceNames>)*\<ClassName>.
- The fully qualified class name MUST have a top-level namespace name, also known as a "vendor namespace".
- The fully qualified class name MAY have one or more sub-namespace names.
- Each namespace separator is converted to a DIRECTORY_SEPARATOR when loading from the file system.
- Underscores have no special meaning in any portion of the fully qualified class name.
- Alphabetic characters in the fully qualified class name MAY be any combination of lower case and upper case.
- All class names MUST be referenced in a case-sensitive fashion.

It was born from a requirement: develop a website quickly and powerfully.

I know, someone can say "Use Zend Framwork, CakePHP!", but I could reply: "They are very good toolkits, but they aren't the toolkit that I want!" :P

The development model of MToolkit is *rolling release*. I search some people (developer or not) to increase and modify this strategy: my goal is to manage the versioning of this framework. 


The experiences with other toolkits in different platforms have led me to create this toolkit.

MToolkit was born like a mash-up of two frameworks: .NET and Qt. o_O

Yes, the framework of the evil and the desktop framework for excellence.

I have seen some similarities between Laravel and MToolkit, cool! :D

#<a name="install"></a>Install
To have a full installation of the framework, add into your composer.json file:
```json
{
    "require": {
        "mtoolkit/mtoolkit": "0.1.*"
    }
}
```
Or run the console command:
```
composer require mpstyle/mtoolkit
```

#<a name="some_good_features"></a>Some good features
- Completely Object Oriented
- Autoload of classes (PSR-0 and PSR-4 Standard)
- Autorun of pages and of [RPC Json web services](https://github.com/MpStyle/MToolkit/tree/master/Network/RPC/Json) from controller classes
- Javascript frameworks compatibility (jQuery, Bootstrap, AngularJS, etc)
- Master page concept (http://msdn.microsoft.com/it-it/library/system.web.ui.masterpage.aspx)
- Decoupling between business logic and graphics
- Fluent setters

#<a name="mtoolkit_module"></a>MToolkit modules
Like Qt, MToolkit has a lot of modules, one for every type of usage.
Here you are the list:
- [Core](https://github.com/mtoolkit/mtoolkit-core)
- [Network](https://github.com/mtoolkit/mtoolkit-network)
- [Model](https://github.com/mtoolkit/mtoolkit-model)
- [Controller](https://github.com/mtoolkit/mtoolkit-controller)
- [View](https://github.com/mtoolkit/mtoolkit-view)
- [Cache](https://github.com/mtoolkit/mtoolkit-cache)
- [Entity](https://github.com/mtoolkit/mtoolkit-entity)

#<a name="software_using_mtoolkit"></a>Software using MToolkit
- [Back-end of TVGuide](https://play.google.com/store/apps/details?id=net.micene.minigroup.palimpsests.lite)
- [Notification Manager](https://github.com/MpStyle/NotificationManager)
- [TV Guide web site](http://tvguide.micene.net/)

#<a name="lets_start"></a>Let's start

Create a folder for your project.

*composer.json*:
```json
{
  "require": {
    "mpstyle/mtoolkit": "dev-master"
  }
}
```

On the root of your project create a new file (*Settings.php*) with this content:

```php

<?php
require_once __DIR__ . '/vendor/autoload.php';

use MToolkit\Core\MApplication;

class Settings
{
    public static function run()
    {
        // Set the root path of the project
        MApplication::setApplicationDirPath(__DIR__);
    }
}

Settings::run();

```

**This file must be included in every entry page of your project.**

If you use PSR-0 or PSR-4 standard, instead of the following code:
```php
MApplication::setApplicationDirPath(__DIR__);
```
You can use the [Composer autoload](https://getcomposer.org/doc/04-schema.md#autoload). 

## Create a page

Controller (Index.php):

```php
<?php

require_once __DIR__ . '/Settings.php';

use \MToolkit\Controller\MPageController;

class Index extends MAbstractPageController
{
    private $masterPage;

    public function __construct()
    {
        parent::__construct(__DIR__.'/Index.view');
    }

    public function helloWorld()
    {
        return "Hello World";
    }
} 
```

And the *view* file. Every view file must contain the meta tag, with the correct *content-type*:
```html
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
```
*Index.view*:

```php
<?php /* @var $this Index */ ?>
<html>
    <head>
        <title>Entry page</title>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    </head>
    <body>
        <b><?php echo $this->helloWorld(); ?></b>
    </body>
</html>
```

And now you can create your web app.
