---
name: 2C-Auth Information Display
type: knowledge
version: 1.0.0
agent: CodeActAgent
triggers: []
---

# 2C-Auth Information Display Microagent

This microagent provides comprehensive information about the 2C-Auth project, which is a custom fork of Myth\Auth for CodeIgniter 4, maintained by Twocoms Consulting for EDU-ERP 3.0 projects.

## Project Overview

**2C-Auth** is a flexible, powerful, and secure authentication & authorization package for CodeIgniter 4. It's a maintained fork of the original Myth\Auth library, customized specifically for Twocoms Consulting / EDU-ERP 3.0 projects.

## Key Information

### Project Details
- **Repository**: Pream-webapps/2C-auth
- **Original Project**: Myth\Auth by Lonnie Ezell
- **Maintainer**: Twocoms Consulting / EDU-ERP 3.0 Team
- **License**: MIT
- **Type**: Library

### Requirements
- PHP 7.4+, 8.0+
- CodeIgniter 4.1+

### Features
- Password-based authentication with remember-me functionality
- Role-Based Access Control (RBAC) per NIST standards
- Ready-made views for login, registration, forgot/reset password
- Publishable configs & views for customization
- Email-based account verification
- Debug Toolbar integration
- Extendable and customizable for enterprise needs

### Installation
```bash
composer require pream-webapps/2c-auth:dev-develop
```

### Available Services
- **authentication** – Handles login/logout, credential checks
- **authorization** – Handles RBAC roles and permissions
- **passwords** – Strong password validation

### Helper Functions
Load with: `helper('auth');`

Available helpers:
- `logged_in()` → check if user logged in
- `user()` → get User entity
- `user_id()` → get user ID
- `in_groups($groups)` → check group membership
- `has_permission($perm)` → check user permissions

### Configuration Steps
1. **Email Setup**: Edit `app/Config/Email.php` and set `fromEmail` and `fromName`
2. **Validation Rules**: Add password validation rules in `app/Config/Validation.php`
3. **Migrations**: Run `php spark migrate -all`

### Route Filters
Available filters for route protection:
- `login` → \Myth\Auth\Filters\LoginFilter::class
- `role` → \Myth\Auth\Filters\RoleFilter::class
- `permission` → \Myth\Auth\Filters\PermissionFilter::class

### Customization
Run `php spark auth:publish` to copy configs, views, entities into `app/` for modification.

## Project Structure
The project follows standard PHP library structure with:
- `src/` - Main source code
- `tests/` - Unit tests
- `docs/` - Documentation
- `examples/` - Usage examples
- Configuration files for various tools (PHPStan, Psalm, Rector, etc.)

## Important Notice
CodeIgniter now has an official authentication library called CodeIgniter Shield. For new projects, Shield is the recommended option. This fork (pream-webapps/2c-auth) is maintained for existing projects that already rely on Myth\Auth and need customizations.

## Usage Context
This microagent can display comprehensive information about the 2C-Auth project when requested. It provides details about installation, configuration, features, and usage patterns for developers working with this authentication library.