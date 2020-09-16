# This is a fork of [yaapis/Theme](https://github.com/yaapis/Theme) and adds compatibility for Laravel 8.

# Theme support for Laravel 6 / 7 / 8

Inspired by [bigecko/laravel-theme](https://github.com/harryxu/laravel-theme).
Themes are stored inside default laravel's resources folder


## Installation
Require this package in your composer.json:

~~~bash
composer require remzikocak/theme
~~~

Or manually add 

~~~json
"remzikocak/theme": "4.*"
~~~



Optionally, publish config using artisan CLI (if you want to overwrite default config).

~~~bash
php artisan vendor:publish --provider="YAAP\Theme\ThemeServiceProvider"
~~~

## Package config

~~~php
	return array(
        'path'          => base_path('resources/themes'),
        'assets_path'   => 'themes',
    );
~~~


## Theme config

~~~php
	return array(
        'name'         => 'default',
        'inherit'      => null,
    );
~~~



##Usage

### Structure

```
├── themes/
    ├── default/
    |   ├── assets/        
        ├── lang/        
        ├── layouts/
        ├── partials/
        ├── views/
        |   └── hello.blade.php
        └── config.php

    └── admin/

    ├── views/
    |   ├── emails/
    |   |   └── notify.blade.php
    |   └── hello.blade.php

├── public/
    └── themes/
		└── default/
			├── css/
			|	└── styles.css
			└── images/
                └── icon.png
```

### Create theme with artisan CLI

The first time you have to create theme "default" structure, using the artisan command:

~~~bash
php artisan theme:create default
~~~

In order to seed webpack.mix.js with custom rules add --with-mix option

~~~bash
php artisan theme:create default --with-mix
~~~

To delete an existing theme, use the command:

~~~bash
php artisan theme:destroy default
~~~

###Init theme

~~~php
Theme::init($name)
~~~

This will add to views find path:
* themes/{$name}
* themes/{$name}/views

Lang files will be added as well:
* themes/{$name}/lang

### Making view

~~~php
View::make('hello');
View::make('emails.notify');
~~~

### Assets
Use laravel mix for assets.

~~~css
<link rel="stylesheet" href="{{ mix('/themes/default/css/app.min.css') }}"/>
~~~

~~~js
<script type="text/javascript" src="{{ mix('/themes/default/js/app.min.js') }}"></script>
~~~


###Blade templates

```
	@extends('layouts.master')

	@include('partials.header')

	@section('content')

	    <section id="main">
	        <h1>HOME</h1>
	    </section>
	@stop

	@include('partials.footer')

```

###Fallback capability

You still able to use default `View::make('emails.notify')` which is stored outside the themes directory

## Follow us
Stay up to date with the latest Vuestic news! Follow us on [LinkedIn](https://www.linkedin.com/company/hexide-digital) or [Facebook](https://www.facebook.com/hexide.digital)

## License
[MIT](https://github.com/epicmaxco/vuestic-admin/blob/master/LICENSE) license.
