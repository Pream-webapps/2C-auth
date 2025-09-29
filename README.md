Here’s an updated **README.md** tailored for your **custom fork (`pream-webapps/2c-auth`)**.
I’ve preserved the original structure but updated naming, installation instructions, and branding to reflect your fork, while keeping the documentation relevant.

---

# 2C-Auth (Fork of Myth:Auth)

[![PHPUnit](https://github.com/Pream-webapps/2C-auth/workflows/PHPUnit/badge.svg)](https://github.com/Pream-webapps/2C-auth/actions/workflows/phpunit.yml)

Flexible, Powerful, Secure authentication & authorization package for CodeIgniter 4.
This is a maintained fork of [Myth\Auth](https://github.com/lonnieezell/myth-auth) customized for **Twocoms Consulting / EDU-ERP 3.0** projects.

---

## Project Notice

CodeIgniter now has an official authentication library, [CodeIgniter Shield](https://www.codeigniter.com/user_guide/libraries/official_packages.html#shield).
If you are starting a new project from scratch, Shield is the recommended option.

This fork (`pream-webapps/2c-auth`) is maintained for existing projects that already rely on Myth\Auth and need customizations.

---

## Requirements

* PHP 7.4+, 8.0+
* CodeIgniter 4.1+

---

## Features

* Password-based authentication with remember-me functionality
* Role-Based Access Control (RBAC) per NIST standards
* Ready-made views for login, registration, forgot/reset password
* Publishable configs & views for customization
* Email-based account verification
* Debug Toolbar integration
* Extendable and customizable for enterprise needs

---

## Installation

Install directly from this repository via Composer:

```bash
composer require pream-webapps/2c-auth:dev-develop
```

This will add the latest development branch of **2C-Auth** as a module to your project.

---

### Manual Installation (if not using Composer)

1. Clone or download this repo into `app/ThirdParty/2c-auth/`
2. Edit **app/Config/Autoload.php** and add:

```php
$psr4 = [
    'Config'      => APPPATH . 'Config',
    APP_NAMESPACE => APPPATH,
    'App'         => APPPATH,
    'Myth\Auth'   => APPPATH . 'ThirdParty/2c-auth/src',
];
```

---

## Configuration

After installation:

1. **Email Setup**
   Edit `app/Config/Email.php` and set `fromEmail` and `fromName`.

2. **Validation Rules**
   Add password validation rules in `app/Config/Validation.php`:

   ```php
   \Myth\Auth\Authentication\Passwords\ValidationRules::class
   ```

3. **Migrations**
   Run database migrations:

   ```bash
   php spark migrate -all
   ```

---

## Routes

Default routes are auto-loaded from `Config/Routes.php`.
To override, copy the file into `app/Config/Routes.php` and customize.

---

## Views

Default views are based on Bootstrap.
To override, edit `app/Config/Auth.php` and change the `$views` mapping to your custom views (e.g., `app/Views/Authentication/...`).

---

## Services

Available services:

* **authentication** – Handles login/logout, credential checks
* **authorization** – Handles RBAC roles and permissions
* **passwords** – Strong password validation

Example:

```php
$authenticate = service('authentication');
$authorize    = service('authorization');
```

---

## Helper Functions

Load with:

```php
helper('auth');
```

Available helpers:

* `logged_in()` → check if user logged in
* `user()` → get User entity
* `user_id()` → get user ID
* `in_groups($groups)` → check group membership
* `has_permission($perm)` → check user permissions

---

## Users

* Uses **Entities** (`Myth\Auth\Entities\User`)

* `UserModel` supports role assignment:

  ```php
  $user = $userModel
              ->withGroup('guests')
              ->insert($data);
  ```

* Default group can be set in `Config\Auth::$defaultUserGroup`

---

## Restricting Routes

Filters available in `Config\Filters.php`:

```php
'login'      => \Myth\Auth\Filters\LoginFilter::class,
'role'       => \Myth\Auth\Filters\RoleFilter::class,
'permission' => \Myth\Auth\Filters\PermissionFilter::class,
```

Use in routes:

```php
$routes->get('admin/users', 'UserController::index', ['filter' => 'role:admin']);
```

Or apply globally in `Config\Filters`.

---

## Customization

* Run:

  ```bash
  php spark auth:publish
  ```

  to copy configs, views, entities into `app/` for modification.
* Extend controllers/models/entities as needed.

---

## Credits

* Original project: [Myth\Auth](https://github.com/lonnieezell/myth-auth) by Lonnie Ezell
* Fork maintained by: **Twocoms Consulting / EDU-ERP 3.0 Team**

---

✨ Now your README makes it clear this is a **custom fork** (`pream-webapps/2c-auth`) while still keeping all the Myth\Auth documentation intact.

---

Do you want me to also add a **“Differences from original Myth\Auth”** section (listing what’s customized in your fork, like extra fields or changed namespaces), so future developers can see what’s unique to your version at a glance?
