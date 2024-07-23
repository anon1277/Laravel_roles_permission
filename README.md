# Laravel Roles and Permissions

This project is a Laravel application that implements role-based access control (RBAC) using the Spatie Laravel Permission package.

## Table of Contents

- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Middleware](#middleware)
- [Blade Directives](#blade-directives)
- [Contributing](#contributing)
- [License](#license)

## Installation

Follow these steps to set up the project.

### Prerequisites

- PHP 8.1 or higher
- Composer
- MySQL or any other supported database

### Steps

1. **Clone the repository**

    ```bash
   git@github.com:anon1277/Laravel_roles_permission.git
    cd your-repo-name
    ```

2. **Install dependencies**

    ```bash
    composer install
    ```

3. **Set up the environment file**

    Copy the `.env.example` file to `.env` and fill in your database and other configurations.

    ```bash
    cp .env.example .env
    ```

4. **Generate application key**

    ```bash
    php artisan key:generate
    ```

5. **Run migrations**

    ```bash
    php artisan migrate
    ```

6. **Install and configure Spatie Laravel Permission**

    Publish the configuration file:

    ```bash
    php artisan vendor:publish --provider="Spatie\Permission\PermissionServiceProvider"
    ```

    Run the command to create the roles and permissions tables:

    ```bash
    php artisan migrate
    ```

## Configuration

### Creating Roles and Permissions

Create roles and permissions using the following commands or directly in your database seeders.

```php
use Spatie\Permission\Models\Role;
use Spatie\Permission\Models\Permission;

// Creating a role
$role = Role::create(['name' => 'admin']);

// Creating a permission
$permission = Permission::create(['name' => 'edit articles']);

// Assign permission to role
$role->givePermissionTo($permission)


//Assigning Roles to Users
You can assign roles to users using the following methods:

---

```php
use App\Models\User;

$user = User::find(1);
$user->assignRole('admin');


//Usage
//Checking Roles and Permissions
//Check if a user has a specific role or permission:


$user->hasRole('admin'); // returns boolean
$user->hasPermissionTo('edit articles'); // returns boolean
Middleware
Protect your routes using role and permission middleware:

Route::group(['middleware' => ['role:admin']], function () {
    Route::get('/admin', [AdminController::class, 'index']);
});

Route::group(['middleware' => ['permission:edit articles']], function () {
    Route::get('/articles/edit', [ArticleController::class, 'edit']);
});
//Blade Directives
//Use Blade directives to show or hide content based on roles or permissions:

//blade File code

@role('admin')
    <p>This is visible to users with the admin role.</p>
@endrole

@can('edit articles')
    <p>This is visible to users with the edit articles permission.</p>
@endcan

---

<p align="center"><img src="/art/socialcard.png" alt="Social Card of Laravel Permission"></p>

# Associate users with permissions and roles

[![Latest Version on Packagist](https://img.shields.io/packagist/v/spatie/laravel-permission.svg?style=flat-square)](https://packagist.org/packages/spatie/laravel-permission)
[![GitHub Tests Action Status](https://img.shields.io/github/actions/workflow/status/spatie/laravel-permission/run-tests-L8.yml?branch=main&label=Tests)](https://github.com/spatie/laravel-permission/actions?query=workflow%3ATests+branch%3Amain)
[![Total Downloads](https://img.shields.io/packagist/dt/spatie/laravel-permission.svg?style=flat-square)](https://packagist.org/packages/spatie/laravel-permission)

## Documentation, Installation, and Usage Instructions

See the [documentation](https://spatie.be/docs/laravel-permission/) for detailed installation and usage instructions.

## What It Does
This package allows you to manage user permissions and roles in a database.

Once installed you can do stuff like this:

```php
// Adding permissions to a user
$user->givePermissionTo('edit articles');

// Adding permissions via a role
$user->assignRole('writer');

$role->givePermissionTo('edit articles');
```

Because all permissions will be registered on [Laravel's gate](https://laravel.com/docs/authorization), you can check if a user has a permission with Laravel's default `can` function:

```php
$user->can('edit articles');
```

## Support us

[<img src="https://github-ads.s3.eu-central-1.amazonaws.com/laravel-permission.jpg?t=1" width="419px" />](https://spatie.be/github-ad-click/laravel-permission)

We invest a lot of resources into creating [best in class open source packages](https://spatie.be/open-source). You can support us by [buying one of our paid products](https://spatie.be/open-source/support-us).

We highly appreciate you sending us a postcard from your hometown, mentioning which of our package(s) you are using. You'll find our address on [our contact page](https://spatie.be/about-us). We publish all received postcards on [our virtual postcard wall](https://spatie.be/open-source/postcards).

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Contributing

Please see [CONTRIBUTING](https://github.com/spatie/.github/blob/main/CONTRIBUTING.md) for details.

### Testing

``` bash
composer test
```

### Security

If you discover any security-related issues, please email [security@spatie.be](mailto:security@spatie.be) instead of using the issue tracker.

## Postcardware

You're free to use this package, but if it makes it to your production environment we highly appreciate you sending us a postcard from your hometown, mentioning which of our package(s) you are using.

Our address is: Spatie, Kruikstraat 22, 2018 Antwerp, Belgium.

We publish all received postcards [on our company website](https://spatie.be/en/opensource/postcards).

## Credits

- [Chris Brown](https://github.com/drbyte)
- [Freek Van der Herten](https://github.com/freekmurze)
- [All Contributors](../../contributors)

This package is heavily based on [Jeffrey Way](https://twitter.com/jeffrey_way)'s awesome [Laracasts](https://laracasts.com) lessons
on [permissions and roles](https://laracasts.com/series/whats-new-in-laravel-5-1/episodes/16). His original code
can be found [in this repo on GitHub](https://github.com/laracasts/laravel-5-roles-and-permissions-demo).

Special thanks to [Alex Vanderbist](https://github.com/AlexVanderbist) who greatly helped with `v2`, and to [Chris Brown](https://github.com/drbyte) for his longtime support  helping us maintain the package.

And a special thanks to [Caneco](https://twitter.com/caneco) for the logo ✨

## Alternatives

- [Povilas Korop](https://twitter.com/@povilaskorop) did an excellent job listing the alternatives [in an article on Laravel News](https://laravel-news.com/two-best-roles-permissions-packages). In that same article, he compares laravel-permission to [Joseph Silber](https://github.com/JosephSilber)'s [Bouncer]((https://github.com/JosephSilber/bouncer)), which in our book is also an excellent package.
- [santigarcor/laratrust](https://github.com/santigarcor/laratrust) implements team support
- [ultraware/roles](https://github.com/ultraware/roles) (archived) takes a slightly different approach to its features.
- [zizaco/entrust](https://github.com/zizaco/entrust) offers some wildcard pattern matching

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
