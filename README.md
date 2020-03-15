# Laravel Filterable Trait
Filterable trait for Laravel models. Slightly inspired by
<a href="https://github.com/n7olkachev/laravel-filterable">n7olkachev/laravel-filterable</a>.

**Version**: 0.1.0

## How it works

In POST request, it looks for form fields defained in trait property `filterable_fields` and filter model by them.
If model has defained scope with name of form field it uses that scope.

One can use it in this way:

```php
\App\User::filter()->get()
```

As for now, it can filer collection by three methods - exact filter (is), like filter (like) and range filter (between).


## Installation

You can install the package via composer:

``` bash
composer require stobys/laravel-filterable
```

Next, add Filterable trait and list all filterable properties:

```php
use Filterable;

protected $filterable_fields = [
	'id'			=> 'is',
	'username'		=> 'like',
	'created_at'	=> 'between',
	'created_after'	=> 'scope'
];
```

And voila!


## Examples

```php

class User extends Model
{
    use Filterable;

    protected $filterable_fields = [
        'id'    => 'is',
        'username'    => 'like',
        'created_at'  => 'between',
        'created_after' => 'scope'
    ];

    public function scopeCreatedAfter($query, $time)
    {
        return $query->where('created_at', '>', $time);
    }
}
```


## License

The MIT License (MIT)
